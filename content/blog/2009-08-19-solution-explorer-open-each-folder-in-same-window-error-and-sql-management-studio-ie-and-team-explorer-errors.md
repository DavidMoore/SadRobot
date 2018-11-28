---
author: David
categories:
- Applications
- How To
date: 2009-08-19T20:45:01Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=206
id: 206
tags:
- '{B8DA6310-E19B-11D0-933C-00A0C90DCAA9}'
- '{C90250F3-4D7D-4991-9B69-A5C5BC1C2AE6}'
- actxprxy.dll
- explorer
- ieproxy.dll
- iserviceprovider
- management studio
- no such interface supported
- open each folder
- same window
- sourcegear
- sql server
- team explorer
- vault
title: 'Solution: Explorer open each folder in same window error and SQL Management
  Studio, IE and Team Explorer errors'
url: /blog/2009/08/19/solution-explorer-open-each-folder-in-same-window-error-and-sql-management-studio-ie-and-team-explorer-errors/
aliases: /2009/08/19/solution-explorer-open-each-folder-in-same-window-error-and-sql-management-studio-ie-and-team-explorer-errors/
---

<h2>Problem(s):</h2> <ul> <li>When attempting to open a folder in <strong>Windows Explorer</strong>, the folder opens in a new window, even if "<strong>Open each folder in the same window</strong>" is selected in Folder Options.</li> <li>Some links in <strong>Internet Explorer</strong> don't open correctly</li> <li><strong>Microsoft SQL Server Management Studio</strong>: An error with a message like "Unable to cast COM object of type 'System._\_ComObject' to interface type 'Microsoft.VisualStudio.OLE.Interop.<strong>IServiceProvider'</strong>. This operation failed because the QueryInterface call on the COM component for the interface with IID '{6D5140C1-7436-11CE-8034-00AA006009FA}' failed due to the following error: <strong>No such interface supported</strong> (Exception from HRESULT: 0x80004002 (E\_NOINTERFACE)). (Microsoft.VisualStudio.OLE.Interop)</li> <li><strong>Visual Studio Team Explorer</strong>: When browsing using the Team Explorer window, you may get COM errors similar to those in the SQL Management Studio error above</li> </ul> <h2>Explanation:</h2> I'm not sure of the exact details, but this is what I think I've found. Perhaps someone at Microsoft would correct or elaborate on this. Previously, <strong>actxprxy.dll</strong> (ActiveX Interface Marshaling Library) was used as the proxy for a multitude of system interfaces, such as IShellFolder and IServiceProvider. In Windows 7 (and probably Vista also), the GUID of this library has changed from <em>{B8DA6310-E19B-11D0-933C-00A0C90DCAA9}</em> to <em>{C90250F3-4D7D-4991-9B69-A5C5BC1C2AE6}</em> Secondly, there is also a new Proxy/Stub provider found in <strong>ieproxy.dll</strong> of Internet Explorer (IE ActiveX Interface Marshaling Library). Some interfaces that previously used actxprxy.dll are now registered to use ieproxy.dll. Now various problematic software (such as Vault 3.x) will try to register against actxproxy using the old GUID, and for interfaces now proxied by ieproxy.dll. <h2>Solution</h2> <h3>Solution 1</h3> You must use regsvr32 to re-register the two proxy DLLs, then <strong>reboot</strong> You can use the below batch file to do this. You must run this batch file with administrative privileges (right click on the file and choose <strong>Run as administrato</strong>r): <a href="http://www.davidmoore.info/wp-content/uploads/2009/08/RunAsAdministrator.png"><img class="alignnone size-full wp-image-209" title="RunAsAdministrator" src="http://www.davidmoore.info/wp-content/uploads/2009/08/RunAsAdministrator.png" alt="RunAsAdministrator" width="239" height="96" /></a> If you don't run the batch file as an administrator, you will get an error as pictured: <a href="http://www.davidmoore.info/wp-content/uploads/2009/08/ActxprxyRegisterError.png"><img class="alignnone size-full wp-image-208" title="ActxprxyRegisterError" src="http://www.davidmoore.info/wp-content/uploads/2009/08/ActxprxyRegisterError.png" alt="ActxprxyRegisterError" width="366" height="199" /></a> [<a href="http://www.davidmoore.info/wp-content/uploads/2009/12/RegisterActxprxyAndIeproxy.zip">Download RegisterActxprxyAndIeproxy.cmd</a>] RegisterActxprxyAndIeproxy.cmd source: <pre>@echo off :: 32 bit and 64 bit IF EXIST "%SystemRoot%System32actxprxy.dll" "%SystemRoot%System32regsvr32.exe" "%SystemRoot%System32actxprxy.dll" IF EXIST "%ProgramFiles%Internet Explorerieproxy.dll" "%SystemRoot%System32regsvr32.exe" "%ProgramFiles%Internet Explorerieproxy.dll" :: 64 bit only (32bit on 64 bit) IF EXIST "%WinDir%SysWOW64actxprxy.dll" "%WinDir%SysWOW64regsvr32.exe" "%WinDir%SysWOW64actxprxy.dll" IF EXIST "%ProgramFiles(x86)%Internet Explorerieproxy.dll" "%WinDir%SysWOW64regsvr32.exe" "%ProgramFiles(x86)%Internet Explorerieproxy.dll"</pre> <strong>Don't forget to reboot</strong> after re-registering the DLLs! <em>Edit: The script has been updated to support 64-bit Windows</em> <h3>Solution 2</h3> Some people have reported that � the following command may fix the problem when Solution 1 does not work (first mentioned by snir in the comments): <ol> <li>Open up a Command Prompt (presumably in Administrator � mode) <strong>Start</strong> > <strong>Programs</strong> > <strong>Accessories</strong> > <strong>Command Prompt</strong></li> <li>Type in <strong>sfc /scannow</strong> and hit <strong>Enter</strong></li> </ol> For those for which this solution works, I'd like for someone to find what file(s) were affected and repaired, so we can get a more specific solution and see if it's related to Solution 1. This solution was one I looked at <em>before</em> I made this post which did not work for me. <em> </em>