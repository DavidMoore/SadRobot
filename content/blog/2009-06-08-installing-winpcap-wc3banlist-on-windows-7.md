---
author: David
categories:
- Applications
date: 2009-06-08T19:47:16Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=193
id: 193
tags:
- dota
- frozen throne
- uac
- user account control
- warcraft
- wc3banlist
- win7
- windows 7
- winpcap
title: Installing WinPcap &amp; WC3Banlist on Windows 7
url: /blog/2009/06/08/installing-winpcap-wc3banlist-on-windows-7/
aliases: /2009/06/08/installing-winpcap-wc3banlist-on-windows-7/
---

I had a bit of trouble getting WC3Banlist (mainly due to its dependency on WinPcap) on Windows 7 This is working on Windows 7 RC1, with User Acount Control (UAC) on (set to Default) I did quite a few things when troubleshooting so it's hard to replicate the exact steps, but here's some instructions on how I have it set up now: <h2>Install WinPcap</h2> <ol> <li><a title="Download WinPcap" href="http://www.winpcap.org/install/bin/WinPcap\_4\_1\_beta5.exe" target="\_blank">Download WinPcap 4.1</a></li> <li>Right click the downloaded installer exe and choose <strong>Properties</strong></li> <li>Go to the <strong>Compatibility</strong> tab</li> <li>In <em>Compatibility mode</em>, Tick "<strong>Run this program in compatibility mode for:</strong>" and choose <strong>Windows Vista (Service Pack 2)</strong> from the drop-down</li> <li>Tick "<strong>Run this program as an administrator</strong>" in Privilege Level</li> <li>Hit <strong>OK</strong></li> <li>Run the exe and go through the normal installation</li> </ol> <h2>Install WC3Banlist</h2> <ol> <li><a title="Download Wc3Banlist" href="http://www.wc3banlist.de/downloads.php" target="_blank">Download WC3Banlist</a></li> <li>Right click the installation file and choose <strong>Run as administrator</strong></li> <li>Untick "<strong>Install WinPcap 3.1 (required)</strong>" when you get to the "<em>Select additional tasks</em>" step and proceed as normal</li> </ol> <h2>Run Wc3Banlist</h2> <ol> <li>Browse to where you installed banlist and open up file properties for wc3banlist.exe</li> <li>Go to the <strong>Compatibility</strong> tab and tick <strong>Run as an administrator</strong></li> <li>Click <strong>OK</strong></li> <li>Run wc3banlist.exe</li> </ol> <h2>Verify</h2> <ol> <li>Go to the <strong>Preferences</strong> tab in Wc3Banlist</li> <li>Select <strong>Network</strong> in the list on the left navigation pane</li> <li>Ensure your network card(s) are listed in the drop-down</li> <li>You can click <strong>Diagnostics</strong> to verify banlist can receive TCP packets</li> </ol> <h2>Troubleshooting</h2> If this still isn't working, I would recommend turning off UAC and trying again. <ol> <li>To turn off UAC, open the Control Panel (<strong>Start</strong> > <strong>Control Panel</strong>)</li> <li>Click <strong>System and Security</strong></li> <li>Under <em>Action Center</em>, click <strong>Change User Account Control settings</strong></li> <li>Drag the slider down to <strong>Never Notify</strong></li> <li>Click <strong>OK</strong></li> <li>You <strong>have to restart</strong> for this to take effect</li> </ol>