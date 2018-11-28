---
author: David
categories:
- .net
- WiX
date: 2010-06-30T17:09:49Z
guid: http://www.davidmoore.info/2010/06/30/how-to-detect-if-the-visual-c-2010-redistributable-package-is-installed-with-wix-2/
id: 302
tags:
- "2010"
- how to
- msi
- redistributable
- vc
- visual c++
- wix
title: 'HOW TO: Detect if the Visual C++ 2010 redistributable package is installed
  with WiX'
url: /blog/2010/06/30/how-to-detect-if-the-visual-c-2010-redistributable-package-is-installed-with-wix-2/
aliases: /2010/06/30/how-to-detect-if-the-visual-c-2010-redistributable-package-is-installed-with-wix-2/
---

As noted by Aaron Stebner, there is now a registry key you can search for to detect if the Visual C++ 2010 redistributable package is installed a machine, when installing your application.

There are 3 different (but very similar) registry keys for each of the 3 platform packages. Each key has a DWORD value called "Installed" with a value of 1.

  * HKLMSOFTWAREMicrosoftVisualStudio10.0VCVCRedistx86
  * HKLMSOFTWAREMicrosoftVisualStudio10.0VCVCRedistx64
  * HKLMSOFTWAREMicrosoftVisualStudio10.0VCVCRedistia64

Here's an example of using this in WiX, detecting the presence of the x86 version of the redistributable:

<pre style="font-family: consolas;"><span style="color: blue;">&lt;?</span><span style="color: #a31515;">xml</span><span style="color: blue;"> </span><span style="color: red;">version</span><span style="color: blue;">=</span>"<span style="color: blue;">1.0</span>"<span style="color: blue;"> </span><span style="color: red;">encoding</span><span style="color: blue;">=</span>"<span style="color: blue;">utf-8</span>"<span style="color: blue;">?&gt;
</span><span style="color: blue;">    &lt;</span><span style="color: #a31515;">Include</span><span style="color: blue;">&gt;</span><span style="color: blue;">
        &lt;!--</span><span style="color: green;"> Visual C++ 2010 x86 </span><span style="color: blue;">--&gt;</span><span style="color: blue;">
        &lt;</span><span style="color: #a31515;">Property</span><span style="color: blue;"> </span><span style="color: red;">Id</span><span style="color: blue;">=</span>"<span style="color: blue;">HASVCPP2010</span>"<span style="color: blue;">&gt;
</span><span style="color: blue;">        &lt;</span><span style="color: #a31515;">RegistrySearch</span><span style="color: blue;"> </span><span style="color: red;">Id</span><span style="color: blue;">=</span>"<span style="color: blue;">HasVCPP2010Search</span>"<span style="color: blue;"> </span><span style="color: red;">Root</span><span style="color: blue;">=</span>"<span style="color: blue;">HKLM</span>"<span style="color: blue;"> </span><span style="color: red;">Key</span><span style="color: blue;">=</span>"<span style="color: blue;">SOFTWAREMicrosoftVisualStudio10.0VCVCRedistx86</span>"<span style="color: blue;"> </span><span style="color: red;">Name</span><span style="color: blue;">=</span>"<span style="color: blue;">Installed</span>"<span style="color: blue;"> </span><span style="color: red;">Type</span><span style="color: blue;">=</span>"<span style="color: blue;">raw</span>"<span style="color: blue;"> /&gt;</span><span style="color: blue;">
    &lt;/</span><span style="color: #a31515;">Property</span><span style="color: blue;">&gt;</span><span style="color: blue;">    
    &lt;</span><span style="color: #a31515;">Condition</span><span style="color: blue;"> </span><span style="color: red;">Message</span><span style="color: blue;">=</span>"<span style="color: blue;">This application requires Microsoft Visual C++ 2010 Redistributable Package (x86).</span>"<span style="color: blue;">&gt;</span>Installed OR (HASVCPP2010)<span style="color: blue;">&lt;/</span><span style="color: #a31515;">Condition</span><span style="color: blue;">&gt;</span><span style="color: blue;">
&lt;/</span><span style="color: #a31515;">Include</span><span style="color: blue;">&gt;</span></pre>

When someone runs your installer and they don’t have this package installed, they will get something like this message box when the installer initializes:

[<img style="display: inline; border: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/06/image_thumb.png" border="0" alt="image" width="244" height="115" />](http://www.sadrobot.co.nz/wp-content/uploads/2010/06/image.png)

It’s a good idea to have a setup bootstrapper that automatically installs this package if it’s missing, but this WiX snippet is a good safe-guard for if someone directly runs your MSI.

**Reference**: <http://blogs.msdn.com/b/astebner/archive/2010/05/05/10008146.aspx>