---
author: David
categories:
- Unreal Tournament
date: 2014-09-05T23:26:35Z
guid: http://www.davidmoore.info/blog/?p=1491
id: 1491
tags:
- unreal
- unreal engine
- uproject
- ut
title: Fix the missing right click menu for Unreal Engine Projects (.uproject)
url: /blog/2014/09/05/fix-the-missing-right-click-menu-for-unreal-engine-projects-uproject/
aliases: /2014/09/05/fix-the-missing-right-click-menu-for-unreal-engine-projects-uproject/
---

When you right click on an Unreal Engine project file (.uproject), these is the kind of menu options you should see:

<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://www.davidmoore.info/blog/wp-content/uploads/2014/09/image.png" alt="image" width="479" height="167" border="0" />

But what do you do if you only see this? :

<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://www.davidmoore.info/blog/wp-content/uploads/2014/09/image1.png" alt="image" width="435" height="148" border="0" />

The right click context menu is set up via the Windows Registry.

You could get someone to export their working keys for you, but their installation paths may be different to yours.

I’ve created a Windows batch file instead which will:

  1. Try to find the Unreal Engine installation path on your machine
  2. Add the necessary registry keys to register the Unreal Project type, and the right click options.

You need to make sure the batch file is run with administrator privileges, as it needs to write to HKLM.

You can download the batch file (zipped up): [Unreal Project Menu Registration](http://www.davidmoore.info/blog/wp-content/uploads/2014/09/UnrealProjectMenuRegistration.zip).

Here’s the source code:



&nbsp;