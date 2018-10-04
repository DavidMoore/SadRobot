---
id: 506
title: Windows File Sharing
date: 2011-08-12T22:20:05+00:00
author: David
guid: http://www.davidmoore.info/how-to/windows-file-sharing/
---
So, you want to share your files on the lan without requiring people to log in or join your Home Group?

The following instructions are for Windows 7 and the NTFS (default and recommended) file system.

## Turn off Simple File Sharing

From the **Control Panel**, search for _Folder Options_ and open it (or from an Explorer window, go to the menu **Organize** > **Folder and search options**

Go to the **View** tab

Scroll down the list, and make sure the **Use Sharing Wizard (Recommended)** option is _un-checked_ as in the screenshot:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb2.png" width="400" height="485" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image2.png)

## Enable the Guest account

From the **Control Panel**, search for **Guest** and click on **Turn guest account on or off**:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb3.png" width="244" height="117" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image3.png)

Click on the Guest account:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb4.png" width="244" height="110" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image4.png)

Click to **Turn On** the Guest account:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb5.png" width="244" height="162" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image5.png)

## Give Guest account network access privileges

Bring up the **Run** dialog by going to **Start** > **Run** or hit the **Windows key + R** shortcut

Type in **gpedit.msc** and hit Enter or click **OK**

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb23.png" width="244" height="136" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image23.png)

Expand the nodes as shown in the screenshot until you can select the **User Rights Assignment** under **Local Computer Policy** > **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies**

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb7.png" width="244" height="213" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image7.png)

From the action pane, double-click the **Deny access to this computer from the network** item:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb8.png" width="244" height="74" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image8.png)

If the **Guest** account or **Guests** group are in the list, select them and click **Remove**

## Configure Share

Locate the folder you wish to share in Explorer

Right click the folder and choose **Share with** > **Advanced sharing…**

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb24.png" width="244" height="69" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image24.png)

> Alternatively, you can open the Folder properties and select the Sharing tab.

Click the **Advanced Sharing…** button

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb10.png" width="190" height="244" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image10.png)

Tick **Share this folder**

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb11.png" width="242" height="244" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image11.png)

Click **Permissions**

The default permissions grant _Everyone_ **Read** access (the Everyone group contains Guest).

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb12.png" width="202" height="244" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image12.png)

If you wish to give people any write access at all, it’s recommended you tick Allow for Full Control and use the NTFS Security as the place to configure permissions.

> The reason for this is that even if someone may have Full Control on the share, they _still need the required NTFS permissions_. This allows you to focus on the fine-grained NTFS permissions on your share folder and files and not have to worry about the share permissions at all, without compromising security.
> 
> This also means if you want to give guests modify or create writes on _specific folders or files_ in the share, you can do that in their file permissions without having to configure additional shares.

Click **OK** to close the Permissions for the share, and then click **OK** in the Advanced Sharing dialog to finish creating the share and take you back to the Folder Properties.

Don’t close the Folder properties yet.

## Configure NTFS Permissions

### Give the Guests NTFS access to the files

Go to the **Security** tab for the folder.

Click **Edit**

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb13.png" width="190" height="244" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image13.png)

Click the **Add…** button, type in _Guests_ and click **OK**

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb14.png" width="244" height="73" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image14.png)

This adds the Guests group (which includes Guest), and gives it Read permissions by default:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb15.png" width="244" height="132" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image15.png)

> If you wish to give Guests write access to create, delete and/or modify files and folders, tick **Allow** for **Modify** also.

Click the **OK** button when you’re done.

### Apply permissions to the share’s folders and files

> We must ensure the permissions have been propagated to the folders and files in the share, so that we don’t run into problems with guests not seeing particular folders or files in the share, or seeing them but not being able to access them.
> 
> You may occasionally have to repeat this step when you transfer or create new files or folders in the share, and guests report having trouble accessing them.

Click the **Advanced** button.

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb16.png" width="190" height="244" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image16.png)

Click the **Change Permissions…** button on the Permission tab

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb17.png" width="227" height="134" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image17.png)

Ensure that **Replace all child object permissions with inheritable permissions from this object is checked**, then hit **OK**.

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb18.png" width="244" height="84" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image18.png)

Click **Yes** to continue.

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb19.png" width="244" height="104" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image19.png)

> Depending on the number of files and folders in your share and the speed of your machine, this may take a little while to apply.

Once that is done, you can click **OK** to close the Advanced Security Settings for the share, then click **Close** to close the share folder properties.

## Troubleshooting

You can view what folders and files are being shared, as well as open sessions and files, using the **Computer Management** console.

You can open this by right clicking on **Computer** in the **Start Menu** (or Explorer) and choosing **Manage**.

> You can also get to the Computer Management Console by going to Start > Run, typing in compmgmt.msc and hitting Enter or clicking OK.

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb20.png" width="244" height="93" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image20.png)

Expand the **Shared Folders** node.

### Shares

The **Shares** group lists your current shares, their folder path and the number of clients connected. From here you can right click to **Stop Sharing** a share.

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb21.png" width="244" height="47" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image21.png)

> Note that you’ll see default _ADMIN$_, IPC$, _C$_ and additional ‘_$’_ shares for each physical drive on your machine. Don’t be alarmed; these are administrative shares are should not be removed. No one but computer administrators with logon privileges can access them.

### Sessions

The **Sessions** group lists the current sessions in action, including who the users are, the Computer they’re logging on from, the number of files they have open, the time they’ve been connected to your share, and importantly if they’re logged on as a Guest or not.

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image_thumb22.png" width="244" height="49" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/08/image22.png)

Right clicking an entry in here gives you the option to **Close Session**, (or right click in an empty area in the list to **Disconnect All Sessions**) which can help when you want to get people to re-authenticate when troubleshooting.

### Open Files

**Open Files** is similar to the Sessions group, but gives you more detail on the folders and files opened by various accounts, and the kind of access they’re opening the folders and files with.

Right clicking on open files lets you choose to **Close Open File**, and right clicking in an empty part of the pane gives you the **Disconnect All Open Files** option.