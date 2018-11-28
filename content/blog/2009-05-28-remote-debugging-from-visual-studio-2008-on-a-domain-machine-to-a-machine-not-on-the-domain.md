---
author: David
categories:
- .net
- How To
- Software Development
date: 2009-05-28T17:25:27Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=166
id: 166
tags:
- .net
- attach
- debug
- domain
- local
- machine
- remote
- remote debugger
- remote debugging
- visual studio
- vs
title: Remote debugging from Visual Studio 2008 on a domain machine to a machine not
  on the domain
url: /blog/2009/05/28/remote-debugging-from-visual-studio-2008-on-a-domain-machine-to-a-machine-not-on-the-domain/
aliases: /2009/05/28/remote-debugging-from-visual-studio-2008-on-a-domain-machine-to-a-machine-not-on-the-domain/
---

This details how you can debug an application running on a remote machine from Visual Studio on your local machine, as if the remote application was running on your local machine. The keys are: <ol> <li>There must be a user account with the same username and password on the remote machine and the local machine (MACHINE account, not domain account).</li> <li>Visual Studio 2008 Remote Debugger must be installed and running on the remote machine under the user account in point 1</li> </ol> <h2>Create local machine account</h2> <ol> <li>Right click My Computer > Manage</li> <li>Expand Computer Management > System Tools > Local Users and Groups</li> <li>Right-click Users under Local Users and Groups and choose New User&#8230;</li> <li>Enter in the username e.g. DebugUser</li> <li>Enter and confirm the password</li> <li> Un-check "User must change password at next login" and tick "Password never expire"</li> <li>Click Create</li> <li>Click Close</li> </ol> <h2>Create remote machine account</h2> <ol> <li>Log on to the remote machine and repeat the steps for "Create local machine account"</li> <li><em>You must use the same username and password</em></li> <li>Find the user in the Users list and double-click to edit them</li> <li>Go to the Member Of tab</li> <li>Click Add&#8230;</li> <li>Type in Administrators and hit Enter or click OK</li> <li>Click OK</li> </ol> <h2>Run Visual Studio 2008 Remote Debugger</h2> You have several options for launching the Remote Debugger. <ol> <li>If you install Visual Studio 2008, the Remote Debugger folder can be found in %ProgramFiles%Microsoft Visual Studio 9.0Common7IDE. In the Remote Debugger folder are separate folders for the x86 and x64 versions. Perhaps the easiest solution is to share this folder over the network, allowing you to launch the debugger over the network without having to install anything on the remote machine.</li> <li>Alternatively, you can find the Remote Debugger setup on the first disc for the Visual Studio 2008 setup, in a sub folder called Remote Debugger.</li> <li>Or, you can download it from <a href="http://www.microsoft.com/downloads/details.aspx?FamilyID=440ec902-3260-4cdc-b11a-6a9070a2aaab&displaylang=en">here</a></li> </ol> It's a good idea to run this as a Windows application as recommended by the Visual Studio 2008 Remote Debugger Configuration Wizard (and in my opinion easier to troubleshoot). At this point if you're not logged in as the new user you created, you might want to do that now so that you can run the Remote Debugger under them. Once you've followed instructions for installing, run the remote debugger if it isn't already by going to Start > Programs > Microsoft Visual Studio 2008 > Visual Studio Tools > Visual Studio 2008 Remote Debugger. It should say that it's running an instance similar to DebugUser@RemoteMachineName <h2>Connect to the remote machine with Visual Studio</h2> <ol> <li>In Visual Studio on your local machine, go to Debug > Attach to process&#8230;</li> <li>Make sure the Transport drop-down at the top is set to Default</li> <li>In Qualifier, type in the name of the Remote Debugger instance e.g. DebugUser@RemoteMachineName and hit Enter</li> <li>You should then see the list of remote processes in the list and can select the one you want and click Attach.</li> </ol>