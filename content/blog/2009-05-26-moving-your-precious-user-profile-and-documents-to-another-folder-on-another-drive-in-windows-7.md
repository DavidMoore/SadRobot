---
author: David
categories:
- Applications
- How To
date: 2009-05-26T00:42:10Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=149
id: 149
tags:
- documents
- move
- my documents
- profile
- relocate
- user profile
- win7
- windows
- windows 7
title: Moving your precious user profile and documents to another folder on another
  drive in Windows 7
url: /blog/2009/05/26/moving-your-precious-user-profile-and-documents-to-another-folder-on-another-drive-in-windows-7/
aliases: /2009/05/26/moving-your-precious-user-profile-and-documents-to-another-folder-on-another-drive-in-windows-7/
---

One of the things I learned long ago was to always have more than 1 drive or have my single drive partitioned. You keep your programs and operating system on the C drive. On your D drive goes all your data, downloads and anything that you don't want to vanish on you suddenly. A couple of advantages of this are: <ul> <li>This keeps the C drive quite lean if you want to make an image of it. It contains the operating system files and installed software and nothing else.</li> <li>The D drive contains everything in one spot that you can easily set up for a backup procedure</li> <li>If something catastrophic happens to your operating system, you can (mostly) be comfortable with formatting and installing over the C drive without blowing away all your precious music, photos and docs.</li> <li>You can store your favourite software installers and drivers on your D drive which you can reach easily if doing a reinstall &#8211; rather than having to download them all again if starting from scratch.</li> </ul> If you don't partition or have more than one hdd, an operating system failure could mean the hassle of removing your hard drive and backing data up off it on another running machine. Things can be difficult though with the way Windows likes to store the user profile data on the C drive by default like your application data and My Documents. Here are some instructions for changing Windows 7 so that all your user data is stored on your D drive (or wherever you like). This is starting from a clean install of Windows 7 but you could do it from an existing install; just that trying to change the location of an existing user profile is extremely difficult and not recommended (hence the Dummy account): <ol> <li>When prompted to enter a user name in the Windows 7 installer, use a throw-away username rather than your desired username e.g. Dummy</li> <li>Once installed you should be logged in as Dummy</li> <li>Open up C:Users and copy the <strong>Public</strong> and <strong>Default</strong> folders to the new location e.g. D:Users</li> <li>Open up <strong>regedit</strong> and go to the <strong>HKEY\_LOCAL\_MACHINESOFTWAREMicrosoftWindows NTCurrentVersionProfileList</strong> key</li> <li>Change the <strong>Default</strong>, <strong>ProfilesDirectory</strong> and <strong>Public</strong> values to the new location (e.g. replace %SystemDrive% with D:)</li> <li>You should also consider moving the <strong>ProgramData</strong> location too</li> <li>Restart then log on again as Dummy (not sure if this is necessary but just being safe!)</li> <li>Create a new user. This will be your preferred account. Name it what you want and add it to the Administrators group.</li> <li>Log off Dummy and log on as the new user</li> <li>Click the Start Menu and click on your folder name just below the profile grapic and above "Documents". Right click on the folders and go Properties to verify they are stored in D:Users</li> </ol> Now, if your Windows 7 install becomes unrecoverable, you can safely format and install on the C drive and your user profile will remain intact on D.