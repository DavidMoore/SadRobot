---
author: David
categories:
- .net
- How To
- Software Development
date: 2011-08-08T11:32:00Z
guid: http://www.davidmoore.info/2011/08/08/deleting-and-purging-items-from-team-foundation-server/
id: 454
tags:
- delete
- destroy
- purge
- tfs
title: Deleting and purging items from Team Foundation Server
url: /blog/2011/08/08/deleting-and-purging-items-from-team-foundation-server/
aliases: /2011/08/08/deleting-and-purging-items-from-team-foundation-server/
---

When you delete an item from TFS, it’s not actually permanently gone.

You can view deleted items by going to **Tools** > **Options** > **Source Control** > **Visual Studio Team Foundation Server** and checking the **Show deleted items in the Source Control Explorer** option:

[<img style="background-image: none; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb.png" border="0" alt="image" width="244" height="143" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image.png)

You can then see folders and files that have been deleted, which allows you to right click on them to choose **Undelete** (or go to **File** > **Source Control** > **Undelete**).

It's useful to show deleted items by default, but you may find that your source tree ends up a bit clogged with all the deleted files and folders.

You can purge items you want to delete permanently by using the TFS command-line tools.

**TF.EXE** is found with Visual Studio 2010 under **C:Program Files (x86)Microsoft Visual Studio 10.0Common7IDE** for 64 bit machines, and **C:Program FilesMicrosoft Visual Studio 10.0Common7IDE** on 32 bit.

You might find it useful to add that path to your command line.

The commandlet you want to use is **destroy**, which tf.exe can give us info on:

> `C:WindowsSystem32>tf help destroy<br />
TF - Team Foundation Version Control Tool, Version 10.0.30319.1<br />
Copyright (c) Microsoft Corporation.  All rights reserved.</p>
<p>Destroys, or permanently deletes, version-controlled items from Team<br />
Foundation version control.</p>
<p>tf destroy [/keephistory] itemspec1 [;versionspec]<br />
[itemspec2...itemspecN] [/stopat:versionspec] [/preview]<br />
[/startcleanup] [/noprompt] [/silent]<br />
[/login:username,[password]]<br />
[/collection:TeamProjectCollectionUrl]</p>
<p>Versionspec:<br />
Date/Time         D"any .Net Framework-supported format"<br />
or any of the date formats of the local machine<br />
Changeset number  Cnnnnnn<br />
Label             Llabelname<br />
Latest version    T<br />
Workspace         Wworkspacename;workspaceowner`

To run the command, you have to specify the collection URL. An easy way to get this is open your Team Explorer window in Visual Studio (**View** > **Team Explorer**), select the root server node and look in the Properties window at the **Url** property.

Now you need the server name of the folder or file you want to purge. Locate the file or folder in the **Source Control Explorer**, right click and choose **Properties&#8230;**

The **Server Name:** value is what you want and can be selected and copied to the clipboard.

Now you can run the command:

> `tf destroy <strong>$/MyProject/Main/Bin</strong> /collection:http://servername:8080/tfs/myproject<br />
Do you want to destroy $/MyProject/Main/Bin and all of its children? (Yes/No) y<br />
Destroyed: $/MyProject/Main/Bin;X3601<br />
Destroyed: $/MyProject/Main/Bin/Native;X3601`

Now if you refresh in Solution Explorer, the purged items won't even show up anymore.