---
author: David
categories:
- Software Development
date: 2009-01-17T07:01:50Z
guid: http://davidmoore.info/?p=70
id: 70
tags:
- "8080"
- antivirus
- eset
- http
- netstat
- nod32
- proxy
- tcpview
title: ESET NOD32 Antivirus and Proxies
url: /blog/2009/01/17/eset-nod32-antivirus-and-proxies/
aliases: /2009/01/17/eset-nod32-antivirus-and-proxies/
---

Today I'm working on a .NET hobby project.

At a simple level, I'm writing a web proxy implementation, � and was using 8080 as the default port.

When trying to write and run unit tests to make sure my server was binding to this port and shutting down as and when expected, I found I could connect to 8080 even when the proxy wasn't running. Telnet-ing to that port would initiate a connection, and would eventually drop out at varying speeds, and immediately if I hit a key.

I could see nothing in netstat, and I got to the point of shutting down all programs and services I could and it still happened.

I loaded up <a title="TCPView" href="http://technet.microsoft.com/en-us/sysinternals/bb897437.aspx" target="_blank">TCPView</a> and watched it, and saw that an ekrn.exe was doing stuff when I tried to telnet to port 8080. � This is the ESET Service, part of <a title="ESET NOD32 Antivirus Home Page" href="http://www.eset.com/products/nod32.php" target="_blank">ESET NOD32 Antivirus</a>. I had already tried disabling NOD32 Antivirus while troubleshooting, but I went and inspected the options, and sure enough I saw this:

<img class="size-full wp-image-71" title="ESET NOD32 Anti-Virus HTTP Options" src="http://www.sadrobot.co.nz/wp-content/uploads/2009/01/nod32.png" alt="ESET NOD32 Anti-Virus HTTP Options" width="729" height="527" />

To get the above options window, you need to open the main NOD32 window, click **Setup** from the left bar and click **Enter entire advanced setup tree&#8230;**

Eureka! NOD32 sits there and quietly intercepts web requests to the usual web and proxy ports, so that it can appear that there are actually programs listening on those ports when there _aren't_. Even when you've disabled the Web Access Protection and Real-time protection.

So now my options are to choose a new default port for my proxy, or disable 8080 in the NOD32 HTTP options.