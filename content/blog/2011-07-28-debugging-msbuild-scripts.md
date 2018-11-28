---
author: David
categories:
- .net
- Software Development
date: 2011-07-28T14:20:40Z
guid: http://www.davidmoore.info/2011/07/28/debugging-msbuild-scripts/
id: 435
tags:
- debug
- msbuild
title: Debugging MSBuild scripts
url: /blog/2011/07/28/debugging-msbuild-scripts/
aliases: /2011/07/28/debugging-msbuild-scripts/
---

If you want to debug an MSBuild script from without Visual Studio, you need to use the /debug command line option.

The trick is that this option is not normally available; you need to set a registry key to enable it.

## Enable the MSBuild Debugger

Under the **HKLMSoftwareMicrosoftMSBuild4.0** key, create a string value called **EnableDebugger** with a value of “**true**”.

If you’re on a 64 bit system, you’ll also want to set the same value under the key **HKLMSoftwareWow6432NodeMicrosoftMSBuild4.0**.

## Verify

If you then run msbuild /help, you should now see the documentation on the /debug switch:

> <pre>/debug
                    Causes a debugger prompt to appear immediately so that
                    Visual Studio can be attached for you to debug the
                    MSBuild XML and any tasks and loggers it uses.</pre>

## Debugging

Now you can pass the **/debug** option to MSBuild when running it. This will immediately break into the debugger, which will usually give you a prompt to select your JIT debugger:

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/07/image_thumb1.png" border="0" alt="image" width="225" height="244" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/07/image1.png)

The debug session will then start at the very top of the root MSBuild project file, and you can go from there.

You can set breakpoints in your MSBuild project files from within the IDE, and inspect the MSBuild variables using Locals and Watch.

Some more tips:

  * Your breakpoints may not show up to be hit yet until the project file they’re contained in actually loads. If you continue on, the project will get loaded and the breakpoint will get hit.
  * To prevent yourself breaking into framework code that you don’t have source for, you can check the **Enable Just My Code (Managed only)** option under **Debug** > **Options and Settings** > **Debugging** > **General**.
  * From the Immediate window to evaluate conditions using EvaluateCondition:

> <pre>Immediate input: EvaluateCondition("'$(MyProperty)' == ''")
Immediate output: false</pre>

  * From the Immediate window you can evaluate expressions using EvaluateExpression (remember to escape slashes):

> <pre>Immediate input: EvaluateExpression("C:\$(MyFolderName)")
Immediate output: C:MyFolder</pre>

Original article and full details (recommended reading) is here: [http://blogs.msdn.com/b/visualstudio/archive/2010/07/06/debugging-msbuild-script-with-visual-studio.aspx](http://blogs.msdn.com/b/visualstudio/archive/2010/07/06/debugging-msbuild-script-with-visual-studio.aspx "http://blogs.msdn.com/b/visualstudio/archive/2010/07/06/debugging-msbuild-script-with-visual-studio.aspx")