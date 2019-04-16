---
id: 461
title: Debugging Windows Installer Custom Actions
description: How to debug your custom actions using an IDE
date: 2011-08-10T13:34:41+00:00
author: David
guid: http://www.davidmoore.info/?page_id=461
---
## General

First, you must know the name of the custom action you want to debug. In this example we'll call it MyCustomAction.

Set the MsiBreak environment variable (user or system) to the name of the custom action. You can do this easily by running setx from the commandline:
  
  ```batch
  C:\Windows\System32>setx MsiBreak MyCustomAction
  SUCCESS: Specified value was saved.
  C:\Windows\System32>
  ```
Run your installer

You should get now get a message box prompt like this:

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="image" src="/wp-content/uploads/2011/08/image_thumb1.png" border="0" alt="image" width="482" height="173" />](/wp-content/uploads/2011/08/image1.png)

At this point, you can use Visual Studio or another debugger such as WinDBG to attach to the specified process.