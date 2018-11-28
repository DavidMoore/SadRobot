---
author: David
categories:
- Entertainment
date: 2012-01-27T09:49:25Z
guid: http://www.davidmoore.info/2012/01/27/creating-a-machine-account-login-for-sql-server/
id: 520
title: Creating a machine account login for SQL Server
url: /blog/2012/01/27/creating-a-machine-account-login-for-sql-server/
aliases: /2012/01/27/creating-a-machine-account-login-for-sql-server/
---

You can create a machine account login for SQL Server with the following command:

<pre style="padding-bottom: 0px; line-height: normal; width: auto; font-family: ; background: white; color: ; overflow: visible"><font face="Consolas"><span style="color: "><font color="#0000ff">CREATE</font></span>&#160;<span style="color: "><font color="#ff00ff">USER</font></span>&#160;<span style="color: "><font color="#008080">[MACHINENAME]</font></span>&#160;<span style="color: "><font color="#0000ff">FOR</font></span>&#160;<span style="color: "><font color="#0000ff">LOGIN</font></span>&#160;<span style="color: "><font color="#008080">[DOMAIN\MACHINENAME$]</font></span>&#160;<span style="color: "><font color="#0000ff">WITH</font></span>&#160;<span style="color: "><font color="#0000ff">DEFAULT_SCHEMA</font></span><span style="color: "><font color="#808080">=</font></span><span style="color: "><font color="#008080">[dbo]</font></span>
</font></pre>
