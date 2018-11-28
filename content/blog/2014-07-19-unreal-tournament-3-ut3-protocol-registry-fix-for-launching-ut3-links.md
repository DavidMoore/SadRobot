---
author: David
categories:
- Games
- Unreal Tournament
date: 2014-07-19T19:42:33Z
guid: http://www.davidmoore.info/blog/?p=1301
id: 1301
title: Unreal Tournament 3 (UT3) Protocol Registry Fix for launching UT3 links
url: /blog/2014/07/19/unreal-tournament-3-ut3-protocol-registry-fix-for-launching-ut3-links/
aliases: /2014/07/19/unreal-tournament-3-ut3-protocol-registry-fix-for-launching-ut3-links/
---

UT3, at least installed via Steam, doesn't seem to register a URI scheme in Windows so that you can create links to UT3 servers, as was possible in earlier versions of Unreal Tournament.

This can be fixed by manually adding a ut3 protocol to the Windows registry.

## Instructions

  1. Download the initial registry fix, but don't merge it yet: [Download UT3 Protocol registry fix](/downloads/games/ut/ut3protocol.zip)
  2. Open it with a text editor such as Notepad
  3. Change the install location to make where you have UT3. If your steam library is by default C:\Games\Steam, then you won't have to change anything.
  4. Save the file.
  5. Double-click the file to merge it with Windows Registry; click Yes at the warning prompt to proceed.

For information's sake, the contents of the registry file is below. You can create your own registry file from this by copying and saving the text, giving the file a .reg file extension.

```registry
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\unreal]
@="URL:Unreal Tournament 3 Protocol"
"URL Protocol"=""

[HKEY_CLASSES_ROOT\unreal\DefaultIcon]
@="C:\\Games\\Steam\\steamapps\\common\\unreal tournament 3\\Binaries\\UT3.exe,1"

[HKEY_CLASSES_ROOT\unreal\shell]
@="open"

[HKEY_CLASSES_ROOT\unreal\shell\open]

[HKEY_CLASSES_ROOT\unreal\shell\open\command]
@="\"C:\\Games\\Steam\\steamapps\\common\\unreal tournament 3\\Binaries\\UT3.exe\" \"%1\""


```

I will look into automating this to detect where UT3 is installed, but I'm not sure how or where to get this information from Steam programmatically.

# Creating server links

### Format:

> unreal://**serveraddress**:**port**

The address starts with **unreal://**, followed by the **server name** or **IP address**, then the **server port** (default being **7777**).

UT3 apparently only likes the **unreal** protocol; changing it to **ut3** or **ut**, the game complains at launch time about the URL.

### Examples:

  * [ureal://unreal.opla.net.nz:7777](unreal://unreal.opla.net.nz:7777)
  * <unreal://202.160.117.194:7777>