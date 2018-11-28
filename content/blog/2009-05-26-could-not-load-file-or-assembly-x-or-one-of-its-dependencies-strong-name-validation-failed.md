---
author: David
categories:
- .net
- How To
- Software Development
date: 2009-05-26T15:54:34Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=153
id: 153
tags:
- .net
- assembly
- c#
- exception
- failed
- sn
- sn.exe
- strong name
- validation
title: Could not load file or assembly &#226;&#8364;&#732;x&#226;&#8364;&#8482; or
  one of its dependencies. Strong name validation failed.
url: /blog/2009/05/26/could-not-load-file-or-assembly-x-or-one-of-its-dependencies-strong-name-validation-failed/
aliases: /2009/05/26/could-not-load-file-or-assembly-x-or-one-of-its-dependencies-strong-name-validation-failed/
---

In some of the work I'm doing right now, I'm manipulating an assembly after compile time - having it disassembled into IL, tweaked, then re-compiled back into an assembly. The assembly is signed and what is being done to the assembly is breaking the strong name. This is quite comforting to know; the strong name wouldn't be so strong if it was that easy to hack an assembly with a strong name. When trying to load the hacked assembly, I am getting an exception (FileLoadException in this case but I'm guessing this may differ depending on your assembly load method) with the message "Could not load file or assembly 'MyAssemblyName' or one of its dependencies. Strong name validation failed.". The first interesting thing here is that the assembly named in the error message isn't the hacked assembly; the hacked assembly is one of MyAssemblyName's dependencies and is what's triggering the error. <em>Make sure that you check the dependencies of the assembly named in the exception message when troubleshooting. The problem may be with one of the dependencies.</em> In my case the exception isn't a surprise because of what's being done to the assembly. But until I resolve that, how can I get around this for now? You can exclude an assembly from strong name validation for development purposes using the <a title="Strong Name Tool" href="http://msdn.microsoft.com/en-us/library/k5b5tt23(VS.71).aspx">Microsoft (R) .NET Framework Strong Name Utility</a> tool aka sn.exe: <code>"%ProgramFiles%Microsoft SDKsWindowsv6.0Abinsn.exe" -Vr "C:PathToAssembly.dll"</code> Make sure you change the sn.exe path depending on which version of the .NET Framework SDK you have installed. If you're having trouble, get into the � "%ProgramFiles%Microsoft SDKsWindows" dir and search for sn.exe, and use the newest one you can find. You might find it handy to add this as a Post-build event command-line for your project from within Visual Studio in Project Properties > Build Events: <code>"%ProgramFiles%Microsoft SDKsWindowsv6.0Abinsn.exe" -Vr "$(TargetPath)"</code> So how do you switch the strong name validation back on for your assembly? Use the -Vu switch: <code>"%ProgramFiles%Microsoft SDKsWindowsv6.0Abinsn.exe" -Vu "C:PathToAssembly.dll"</code>