---
author: David
categories:
- Software Development
date: 2008-12-09T18:18:46Z
guid: http://davidmoore.info/?p=60
id: 60
tags:
- .net
- performance
- ram
- visual studio
title: Visual Studio Performance
url: /blog/2008/12/09/visual-studio-performance/
aliases: /2008/12/09/visual-studio-performance/
---

I'm running Visual Studio 2008 on a old, single-core laptop with 1GB RAM.

VS is a resource hog, so it's not long before my laptop is struggling having a reasonable size solution in addition to the usual open applications.

There are a few things you can do to try and squeeze a bit more performance out of Visual Studio I've found from various blogs and looking around myself. The first two are the most useful. Don't muck with the other options unless you know what they're going to do.

**Recycle Memory**
  
Perhaps the biggest trick is the simplest: if you **minimize Visual Studio**, it will force a garbage collection, and packing of the memory usage. This can make VS drop from a few hundreds MB of memory usage to 20 or less. Of course things will slow down when you go back into VS as things get reloaded into memory from virtual memory and disk.

**Patch to SP1**
  
Make sure <a href="http://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&displaylang=en" target="_blank">Visual Studio 2005 SP1</a> is installed, for the bug and performance fixes since release.

**Turn off animation**
  
Tools > Options > Environment > General and uncheck Animate environment tools.

**Disable the Navigation Bar**
  
Go to Tools > Options > Text Editor > C# and uncheck Navigation bar under Display.

**Turn off Track Changes**
  
Tools > Options > Text Editor and uncheck Track changes.

**Turn off Track Active item**
  
Tools > Options > Projects and Solutions: uncheck Track Active Item in Solution Explorer.

**Turn off AutoToolboxPopulate.**
  
Tools > Options > Windows Forms Designer: set AutoToolboxPopulate to False.

**Startup with an empty environment**
  
Tools > Options > At startup: Show empty content

**Windows Forms refactoring**
  
Tools > Windows Forms Designer > General: Set “EnableRefactoringOnRename” to false in the Refactoring section