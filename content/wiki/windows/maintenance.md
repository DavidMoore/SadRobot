---
title: Windows Maintenance
description: Tips for keeping Windows running smoothly
toc: true
---

## Deployment Image Servicing and Management tool (DISM)

DISM can be used to mount and service a Windows image from a .wim file, .vhd file, or a .vhdx file or, in some cases, to update a running operating system.

You can use DISM to do various cleanup operations related to installed components, updates and service packs.

### Remove Service Pack backup components after Service Pack installation

After installing a Service Pack, you can clean up backed up components:

``dism /online /cleanup-image /spsuperseded /hidesp``

Note this will make it impossible to uninstall the service pack.

### Remove all superceded components

``dism /online /Cleanup-Image /StartComponentCleanup /ResetBase``

This will clean up updates and service pack components, but mean you cannot uninstall Service Packs or installed Windows Updates.

> Reference: http://blog.brankovucinec.com/2014/11/06/use-dism-to-cleanup-winsxs-after-windows-update/

### Disk maintenance

[Manually schedule a disk checked at next restart](/blog/2011/08/04/manually-schedule-a-disk-check-at-next-restart/)