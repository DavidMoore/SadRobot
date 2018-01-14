---
id: 461
title: Debugging Windows Installer Custom Actions
date: 2011-08-10T13:34:41+00:00
author: David
guid: http://www.davidmoore.info/?page_id=461
---
## General

  1. First, you must know the name of the custom action you want to debug. In this example we'll call it MyCustomAction.
  2. Set the MsiBreak environment variable (user or system) to the name of the custom action. You can do this easily by running setx from the commandline:
  
    > `C:WindowsSystem32>setx MsiBreak MyCustomAction<br />
SUCCESS: Specified value was saved.<br />
C:WindowsSystem32>`

  3. Run your installer

You should get now get a message box prompt like this:

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb1.png" border="0" alt="image" width="482" height="173" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image1.png)

At this point, you can use Visual Studio or another debugger such as WinDBG to attach to the specified process.