---
author: David
categories:
- Applications
- How To
date: 2009-05-27T00:14:13Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=157
id: 157
tags:
- .net
- bittorrent
- bt
- ipfilter
- ipfilter.dat
- ipfilterupdater
- torrent
- utorrent
title: Set up IP filtering in uTorrent and keep your ipfilter.dat up to date easily
url: /blog/2009/05/27/set-up-ip-filtering-in-utorrent-and-keep-your-ipfilterdat-up-to-date-easily/
aliases: /2009/05/27/set-up-ip-filtering-in-utorrent-and-keep-your-ipfilterdat-up-to-date-easily/
---

<blockquote>The IPFilter Updater application now has its own page: <a href="http://www.davidmoore.info/ipfilter-updater/">http://www.davidmoore.info/ipfilter-updater/</a></blockquote> uTorrent is one of the most popular BitTorrent clients out there. In my opinion it's the best. You can set up IP filtering in uTorrent to block bad seeds and peers from a list maintained by the community. <h2>How to set up IP filtering in uTorrent</h2> <ol> <li>Open up uTorrent and go to Options > Preferences from the menu or click the Preferences button in the toolbar</li> <li>Select the Advanced option in the tree</li> <li>Find ipfilter.enabled in the list and make sure it's set to true</li> <li>Click OK</li> </ol> <h2>How to get and update the ipfilter.dat</h2> I've written a simple program that will download the ipfilter.dat from SourceForge and copy it into the file where uTorrent expects it. <a href="http://www.davidmoore.info/wp-content/uploads/2009/05/IPFilterUpdater.png"><img class="alignnone size-medium wp-image-251" title="IPFilterUpdater" src="http://www.davidmoore.info/wp-content/uploads/2009/05/IPFilterUpdater.png" alt="" width="683" height="172" /></a> <a href="/ipfilter-updater/">uTorrent IPFilter Updater</a> [ Requires .NET 3.5 ] <blockquote><strong>UPDATED � 26 Jan 2010</strong>: Now requires .NET 3.5, and allows mirror selection <ol> <li>Extract the files to a folder, and run IPFilter.UI.exe</li> <li>Wait for it to download the mirrors, select the one you want, and click Go</li> <li>Once the file has downloaded and extracted, you can close the window</li> </ol> <h4>Enhancements</h4> <strong>Done:</strong> <ul> <li>Download and extract zip file to speed up the download time and minimize the download usage</li> </ul> <ul> <li>Allow selection of mirror you want to use</li> </ul> <strong>To Do:</strong> <ul> <li>Automation through command-line arguments, for scheduled tasks</li> </ul> Source Code:� <a href="http://github.com/DavidMoore/IP-Filter-Updater/">http://github.com/DavidMoore/IP-Filter-Updater/</a></blockquote> <h2>How to get uTorrent to pick up the new ipfilter.dat</h2> You have two options: <ol> <li>You can simply exit and restart uTorrent to load theIPFilter <strong>or</strong></li> <li>You can leave uTorrent open and reload the IPFilter by selecting the Peers tab, right clicking in the list and choosing Reload IPFilter. Annoyingly you need a selected torrent for this to work.</li> </ol> Looking in the Log should show a message similar to "Loaded ipfilter.dat xxxxxx entries)" Because IP ranges and addresses change often, it's a good idea to update your filter list often too.