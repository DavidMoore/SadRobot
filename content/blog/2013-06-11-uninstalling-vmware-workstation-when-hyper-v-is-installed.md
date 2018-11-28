---
author: David
categories:
- Uncategorized
date: 2013-06-11T13:35:54Z
guid: http://www.sadrobot.co.nz/?p=671
id: 671
title: Uninstalling VMWare Workstation when Hyper-V is installed
url: /blog/2013/06/11/uninstalling-vmware-workstation-when-hyper-v-is-installed/
aliases: /2013/06/11/uninstalling-vmware-workstation-when-hyper-v-is-installed/
---

Well, it was annoying enough that VMWare doesn’t launch on my machine when Hyper-V is installed. I’m skeptical that VMWare wouldn’t run if Hyper-V isn’t running at the same time, and this check just reeks of anti-competition.

Unfortunately for VMWare, that can work against them rather than encourage me to uninstall Hyper-V. That means I’m ditching them for now (mainly as Visual Studio integration with Hyper-V for things like Windows 8 and Windows Phone 8 development is good; not to mention, Hyper-V is built in and doesn’t cost extra).

I went to uninstall VMWare today but got this error:

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2013/06/image_thumb.png" width="463" height="176" />](http://www.sadrobot.co.nz/wp-content/uploads/2013/06/image.png)

Wow! Talk about pain in the ass.

Fortunately a quick search later, Jussi Palo has a simple solution, altering the installer’s lua script to skip this check:

<a title="Remove VMware Workstation or Player when Hyper-V is installed" href="http://blog.jussipalo.com/2012/06/remove-vmware-workstation-or-player.html" target="_blank">Remove VMware Workstation or Player when Hyper-V is installed</a>

And now I can uninstall.