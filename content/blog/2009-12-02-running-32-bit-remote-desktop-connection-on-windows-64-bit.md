---
author: David
categories:
- Applications
- How To
date: 2009-12-02T11:16:27Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=234
id: 234
tags:
- "64"
- 64bit
- mstsc
- mstsc.exe
- remote desktop
- system32
- syswow64
- terminal services
- vista
- windows
- windows 7
- windows7
- x64
- x86
title: Running 32-bit Remote Desktop Connection on Windows 64 bit
url: /blog/2009/12/02/running-32-bit-remote-desktop-connection-on-windows-64-bit/
aliases: /2009/12/02/running-32-bit-remote-desktop-connection-on-windows-64-bit/
---

On Windows Vista 64 and Windows 7 64, there is a 32 bit version of Remote Desktop Connection (Microsoft Terminal Services Client, mstsc.exe) in %SystemRoot%SysWOW64. Running this mstsc.exe will launch the 32 bit process but it will instantly launch the 64-bit mstsc.exe from System32 and shut itself down. This makes it impossible to run Remote Desktop Connection 32 bit. This is a problem when you have 32 bit Terminal Services add-ins (which won't run under 64 bit). <strong>Solution: R</strong><strong>ename the 64-bit mstsc.exe</strong> from System32 to prevent it from replacing the 32-bit process. This is simple if you have rights to rename that file. If you're on NTFS you may get a "<strong>You require permission from TrustedInstaller to make changes to this file</strong>" error. To get by this error, you can take Ownership of the file and give yourself full permissions: <ol> <li>Browse to <strong>%SystemRoot%System32</strong></li> <li>Right click mstsc.exe and choose <strong>Properties</strong></li> <li>Go to the <strong>Security</strong> tab</li> <li>Click <strong>Advanced</strong></li> <li>Go to the <strong>Owner</strong> tab</li> <li>Click <strong>Edit</strong></li> <li>From the "<strong>Change owner to:</strong>" list, choose your user name</li> <li>Click <strong>OK</strong></li> <li>Go to the <strong>Permissions</strong> tab</li> <li>Click <strong>Change Permissions⬦</strong></li> <li>Click <strong>Add</strong></li> <li>Enter your user name and click <strong>OK</strong></li> <li>Tick the box in the <strong>Allow</strong> column for <strong>Full control</strong></li> <li>Click <strong>OK</strong></li> <li>Click <strong>OK</strong></li> <li>A Windows Security warning will come up; click <strong>Yes</strong> to proceed</li> <li>Click <strong>OK</strong></li> </ol> Now, you can rename the file mstsc.exe to something like mstsc.exe.bak Then, you can launch mstsc.exe from %SystemRoot%SysWOW64 and you will have 32-bit Remote Desktop Connection running.