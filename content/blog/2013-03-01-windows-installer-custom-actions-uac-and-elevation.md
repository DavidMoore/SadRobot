---
author: David
categories:
- Setup
- WiX
date: 2013-03-01T09:44:14Z
guid: http://sadrobot.azurewebsites.net/?p=82
id: 82
tags:
- elevation
- msi
- uac
- wix
title: Windows Installer custom actions, UAC and elevation
url: /blog/2013/03/01/windows-installer-custom-actions-uac-and-elevation/
aliases: /2013/03/01/windows-installer-custom-actions-uac-and-elevation/
---

We had a problem this week where a merge module from a third party was causing our installer to fail under UAC.

The installation was being elevated, but the custom actions (which were doing things such as file system and registry operations) were still failing due to security exceptions.

The root cause was that the merge module contained custom actions that were still not being run under the elevated account.

The reason behind this is a common one when scheduling deferred actions; the custom action must have the Impersonate flag set to false.

You can do this in WiX code by setting Impersonate to No:

<pre><p>
  &lt;CustomAction Id="RegisterAspNet4" BinaryKey="WixCA" DllEntry="CAQuietExec"
</p>

<p>
  Execute="deferred" Return="check" <strong><font color="#ff0000">Impersonate="no"</font></strong>/&gt;
  
</p></pre>

The documentation in WiX on the Impersonate attribute reads (emphasis mine):

> This attribute specifies whether the Windows Installer, which executes as LocalSystem, should impersonate the user context of the installing user when executing this custom action. **Typically the value should be 'yes', except when the custom action needs elevated privileges to apply changes to the machine**. 

Being a third party merge module, we had to fix this ourselves by opening up Orca and setting this flag manually.

You can do this by looking at the CustomAction table, finding your custom action in the list, and checking the Type field.

The Type field is a field full of flags, and will show up as a decimal number e.g. 1025.

If you open up Windows Calculator, switch to Programmer (View > Programmer or Alt+3), choose Decimal and enter the number, you can check the bit fields:

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://sadrobot.azurewebsites.net/wp-content/uploads/2013/03/image_thumb.png" width="244" height="225" />](http://sadrobot.azurewebsites.net/wp-content/uploads/2013/03/image.png)

The first bit is set to signify it as an In-Script Execution custom action (type 1).

The 11th bit is set to signify Deferred execution (i.e. instead of running immediately, we schedule when the installer should run our custom action).

The 12th bit (the one I’ve highlighted) is the one that turns off impersonation; this is the bit we need to flip on to disable impersonation for this custom action, so that it runs with elevated privileges.

Being the twelfth bit, that is a value of **2048**, so we can just add that to our value, giving us **3073**:

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://sadrobot.azurewebsites.net/wp-content/uploads/2013/03/image_thumb1.png" width="244" height="225" />](http://sadrobot.azurewebsites.net/wp-content/uploads/2013/03/image1.png)

You can see the No Impersonate bit is now flipped.

You can now update the value in Orca and save the merge module (or create a transform).

## References

<a href="http://blogs.msdn.com/b/rflaming/archive/2006/09/23/768248.aspx" target="_blank">UAC in MSI Notes: The NoImpersonate Bit Mistake</a>&nbsp;

<a href="http://msdn.microsoft.com/en-us/library/windows/desktop/aa368069(v=vs.85).aspx" target="_blank">Custom Action In-Script Execution Options (Windows)</a>