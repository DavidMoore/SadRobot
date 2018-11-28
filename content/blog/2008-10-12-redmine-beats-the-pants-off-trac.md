---
author: David
categories:
- Software Development
date: 2008-10-12T22:29:35Z
guid: http://davidmoore.info/?p=19
id: 19
tags:
- redmine
- subversion
- svn
- trac
title: Redmine beats the pants off Trac
url: /blog/2008/10/12/redmine-beats-the-pants-off-trac/
aliases: /2008/10/12/redmine-beats-the-pants-off-trac/
---

<a title="Trac" href="http://trac.edgewall.org" target="_blank">Trac</a> is an extremely popular free issue tracker / wiki with source control integration. Many open source projects are using it.

I've been using Trac for a long time now, and while it used to be very good, it's too stagnant and is lacking in too many ways.

It doesn't support multiple projects, the ticket workflow is cumbersome, the security and roles are rudimentary at best, and call my superficial, but I just don't like how it looks.

While I got pretty good at setting Trac up with configuration and plugins to work nicely, having to go through this process for every single project is frustrating.

Coming back to do some work for <a title="digitalGenus" href="http://www.digitalgenus.com" target="_blank">dG</a> and trying to set up a cross-continent project workflow, I had the opportunity to actually have a re-evaluation of Trac and any alternatives.

It turns out that there's a "new" kid on the block which provides all that Trac does (with very similar layout and features) while addressing the big lacking points.

Multiple project support (even nested projects), role and user management, calendars, files, documents and more &#8211; on top of the expected source control integration, wiki, issue management etc.

The project is called <a title="Redmine" href="http://www.redmine.org/" target="_blank">Redmine</a>. I'm surprised it hasn't received a bit more buzz, as I think it's superior to the pervasive Trac in nearly every way.

It's written using Ruby on Rails (which I think is also a good point; I'd prefer this over Python for if I find the need to write hacks or plugins).

The downside to this is that it didn't prove very easy to integrate with Apache, so we're letting Apache proxy to the ruby server, which while being very slow, isn't noticeable (at least for me, thousands of kilometres away).

So far it's been good to use. Here's hoping the creators keep the ball rolling on it and don't allow moss to gather.