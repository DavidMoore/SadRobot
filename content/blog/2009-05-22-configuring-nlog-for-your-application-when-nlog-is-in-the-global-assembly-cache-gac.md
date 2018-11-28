---
author: David
categories:
- .net
- How To
- Software Development
date: 2009-05-22T12:28:23Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=140
id: 140
tags:
- .net
- assembly
- c#
- config
- ConfigSectionHandler
- gac
- global assembly cache
- NLog
title: Configuring NLog for your application when NLog is in the Global Assembly Cache
  (GAC)
url: /blog/2009/05/22/configuring-nlog-for-your-application-when-nlog-is-in-the-global-assembly-cache-gac/
aliases: /2009/05/22/configuring-nlog-for-your-application-when-nlog-is-in-the-global-assembly-cache-gac/
---

If you have several applications that are using NLog, it can be a good idea to install NLog into the GAC and reference that. A gotcha you must watch out for is caused by this piece of configuration from the NLog site: <code> <configuration> <configSections> <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog"/> </configSections> <nlog> </nlog> </configuration></code> Because you are not using the strong name for the Assembly-qualified name of ConfigSectionHandler, it's impossible to do a GAC lookup, therefore NLog won't be found and you'll get an application error (even if NLog is actually in the GAC). This means your application will throw an exception when the configuration is loaded; there will be no NLog.dll in your application folder and it can't check the GAC as it doesn't have the strong name of the assembly you want. You can fix this by including the strong name: <code> <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog, Version=1.0.0.505, Culture=neutral, PublicKeyToken=5120e14c03d0593c" /> </code>