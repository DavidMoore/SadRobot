---
author: David
categories:
- Software Development
date: 2008-10-14T12:52:42Z
guid: http://davidmoore.info/?p=28
id: 28
tags:
- .net
- BadImageFormatException
- exception
- vmware
title: System.BadImageFormatException
url: /blog/2008/10/14/systembadimageformatexception/
aliases: /2008/10/14/systembadimageformatexception/
---

I'm currently build the new Overclockers New Zealand website in .NET

I have a nice continuous integration server going smoothly, but my most recent check-in threw up a strange error when running the Unit Tests:

> System.BadImageFormatException : Could not load file or assembly 'Overclockers.Web, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null' or one of its dependencies. The module was expected to contain an assembly manifest.

The server is actually a VMWare instance, but is running a 32-bit version of Windows Server 2003 EE.

After some troubleshooting and searching, I decided to first try to explicitly build for x86 first anyway. This is done in the Project Properties dialog in Visual Studio.

<img class="alignnone" title="Target platform for X86" src="/wp-content/uploads/target-platform-x86.jpg" alt="" width="625" height="371" />

When changing this, make sure you make the change for both Debug and Release configurations.

This seemed to fix the problem.

I suspect this could be because I have some Shell32 interop in one of my shared libraries, and this may have caused problems, and/or the fact I'm running the instance on VMWare.