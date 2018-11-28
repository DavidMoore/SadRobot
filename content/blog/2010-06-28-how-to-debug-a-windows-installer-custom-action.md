---
author: David
categories:
- .net
- Software Development
- WiX
date: 2010-06-28T10:53:58Z
guid: http://www.davidmoore.info/?p=293
id: 293
tags:
- custom action
- debug
- installer
- msi
- msibreak
title: 'HOW TO: Debug a Windows Installer custom action'
url: /blog/2010/06/28/how-to-debug-a-windows-installer-custom-action/
aliases: /2010/06/28/how-to-debug-a-windows-installer-custom-action/
---

## Prerequisites:

  * Determine the name of the custom action you want to debug
  * Ensure you have the source code and debug symbols for your custom action

## Steps

  1. Set the MsiBreak environment variable (user or system) to the name of the custom action. For example:
  
    `<br />
Setx MsiBreak <strong>MyCustomActionName</p>
<p></strong>`
  2. Run your installer
  3. At the point where your custom action is about to run, you should get this message box prompt: 
    [<img class="alignnone size-full wp-image-294" title="Debugging Custom Actions" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/06/debugging-custom-actions.png" alt="" width="478" height="169" />](http://www.sadrobot.co.nz/wp-content/uploads/2010/06/debugging-custom-actions.png)</li> 
    
      * Now you can use Visual Studio or another debugger such as WinDBG to attach to the specified process.
      * Click OK on the message box
      * This should break into your debugger. This is a good time to set your breakpoints in your custom action code.
      * When ready, run/continue the debug session.
      * Your custom action should run and your breakpoint(s) will be hit.</ol> 
    
    ## References:
    
    [Debugging Custom Actions](http://msdn.microsoft.com/en-us/library/aa368264(VS.85).aspx) @ msdn.microsoft.com