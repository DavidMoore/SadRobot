---
author: David
categories:
- How To
date: 2011-08-04T12:02:00Z
guid: http://www.davidmoore.info/?p=445
id: 445
tags:
- check
- chkdsk
- disk
- fsutil
- scan
title: Manually schedule a disk check at next restart
url: /blog/2011/08/04/manually-schedule-a-disk-check-at-next-restart/
aliases: /2011/08/04/manually-schedule-a-disk-check-at-next-restart/
---

You can schedule a chkdsk at reboot time for a drive by using the Windows command line utility [fsutil](http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/fsutil.mspx "FSUtil @ microsoft.com").

You do this by setting the "dirty" flag for a drive, which marks the drive for a chkdsk when you next reboot.

Usage:

> <pre>fsutil dirty query &lt;volume pathname&gt;</pre>

e.g.

> <pre>fsutil dirty set <strong>C:</strong></pre>

You can check if a drive has been marked as dirty by using the query command:

> <pre>fsutil dirty query &lt;volume pathname&gt;</pre>