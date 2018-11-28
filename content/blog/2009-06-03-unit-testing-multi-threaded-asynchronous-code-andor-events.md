---
author: David
categories:
- .net
- How To
- Software Development
date: 2009-06-03T10:50:15Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=171
id: 1461
tags:
- .net
- asynchronous
- c#
- events
- mstest
- nunit
- threading
- unit test
title: Unit testing multi-threaded, asynchronous code and/or events
url: /blog/2009/06/03/unit-testing-multi-threaded-asynchronous-code-andor-events/
aliases: /2009/06/03/unit-testing-multi-threaded-asynchronous-code-andor-events/
---

I've been writing some unit tests recently that test some multi-threaded functionality. Typically this involves hooking up some event handlers then waiting for some asynchronous code to fire the event before proceeding with the unit test and assertions. The <a title="ManualResetEvent Class @ MSDN" href="http://msdn.microsoft.com/en-us/library/system.threading.manualresetevent.aspx">ManualResetEvent class (MSDN)</a> seems a good choice for this, and <a title="Unit Testing Multi-Threaded Asynchronous Events" href="http://jopinblog.wordpress.com/2007/07/10/unit-testing-multi-threaded-asynchronous-events/">this post</a> has a small example of using it in a unit test: <blockquote> <pre><code> [Test()] public void AfterRunAsync() { ManualResetEvent manualEvent = new ManualResetEvent(false); TestTestCase tc = new TestTestCase(1, "", 0, 0); bool eventFired = false; tc.RunCompleted += delegate(object sender, AsyncCompletedEventArgs e) { Assert.IsInstanceOfType(typeof (TestTestCase), sender, "sender is TestCase"); bool passed = tc.Passed; string output = tc.Output; eventFired = true; manualEvent.Set(); }; tc.RunAsync(); manualEvent.WaitOne(500, false); Assert.IsTrue(eventFired, "RunCompleted fired"); } </code></pre> </blockquote>