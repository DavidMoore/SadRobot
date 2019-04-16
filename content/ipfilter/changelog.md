---
title: "Changelog"
description: "History of IPFilter Updater releases and changes"
menu:
    ipfilter:
        parent: ipfilter
        weight: 30
---

## 3.0.0 Beta 2

### New

* Added initial support for eMule

### Improvements

* For troubleshooting, a basic log is written to ipfilter.log
* Downloaded list(s) are now sorted and merged to make the list smaller, more compact and faster to load by P2P clients
* Applications receive their own copy of the ipfilter.dat, formatted to each application's preferred format 

### Changes

* Now installing to <UserDirectory>\AppData\Local\Programs\IPFilter (instead of AppData\Local\IPFilter) to follow the established convention for per-user applications
* The cached ipfilter.dat will now be stored in <UserDirectory>\AppData\Local\Programs\IPFilter\ipfilter.dat

## 3.0.0 Beta 1

#### Fixes

* #40 Automatic update fails due to github SSL/TLS restrictions

#### Changes

* Program updates from GitHub Releases
* Distributing a curated, combined default list available from GitHub Releases page
* Requires .NET 4.5

## 26 Jan 2010

### Changes

* Now requires .NET 3.5, and allows mirror selection
* Zip file support
* Allows list selection