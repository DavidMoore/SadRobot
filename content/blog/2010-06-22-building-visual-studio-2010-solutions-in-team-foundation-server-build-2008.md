---
author: David
categories:
- .net
- Software Development
date: 2010-06-22T10:02:36Z
guid: http://www.davidmoore.info/?p=288
id: 288
title: Building Visual Studio 2010 Solutions in Team Foundation Server Build 2008
url: /blog/2010/06/22/building-visual-studio-2010-solutions-in-team-foundation-server-build-2008/
aliases: /2010/06/22/building-visual-studio-2010-solutions-in-team-foundation-server-build-2008/
---

Visual Studio 2010 and Team Foundation Server 2010 have been out for a while. But what if you still have Team Foundation Server 2008 but want to build Visual Studio 2010 solutions on it?

You can do so by updating the Team Foundation Build Service configuration to use the latest version of MSBuild that comes with the .NET Framework 4.0.

  1. Open up� **%Program Files%Microsoft Visual Studio 9.0Common7IDEPrivateAssembliestfsbuildservice.exe.config** in a text editor
  2. Find the� **MSBuildPath** property, which will likely be empty, and enter the path to the .NET Framework 4.0 folder (C:WINDOWSMicrosoft.NETFrameworkv4.0.30319):<img title="tfsbuild" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/06/tfsbuild.png" alt="" width="661" height="107" />
  3. **Save** the file
  4. Restart the � **Visual Studio Team Foundation Build** service

Reference: <http://blogs.msdn.com/b/jimlamb/archive/2009/11/03/upgrading-tfs-2008-build-definitions-to-tfs-2010.aspx>