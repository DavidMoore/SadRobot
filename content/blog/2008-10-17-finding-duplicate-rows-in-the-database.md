---
author: David
categories:
- Software Development
date: 2008-10-17T11:39:40Z
guid: http://davidmoore.info/?p=32
id: 32
tags:
- database
- duplicates
- sql
title: Finding duplicate rows in the database
url: /blog/2008/10/17/finding-duplicate-rows-in-the-database/
aliases: /2008/10/17/finding-duplicate-rows-in-the-database/
---

**NOTE**: This post has been re-visited in [Finding duplicated data across one or more columns in a database table](/2009/02/28/finding-duplicated-data-across-one-or-more-columns-in-a-database-table/)

Information gleaned from Microsoft KB article: <a title="How to remove duplicate rows from a table in SQL Server" href="http://support.microsoft.com/default.aspx?scid=kb;en-us;139444" target="_blank">How to remove duplicate rows from a table in SQL Server</a>

When you allow duplicated rows in a database that aren't expected and shouldn't be allowed, it's a flag saying that you need a unique index on the table to prevent duplicate rows to be added in the first place.

The first step to fixing the problem is to find and fix the duplicated rows.

The second step is to add an index once the existing duplicate rows have been dealt with, so that the problem won't occur in the future.

If you have a "Users" table, which has an "Email" column, you will likely want that Email to have a unique index. You can find the duplicated Emails (and the number of times each email occurs) using this query:

> SELECT **Email**, COUNT(**Email**) AS NumberOfDuplicates FROM \`**Users**\` GROUP BY **Email** HAVING ( COUNT(**Email**) > 1 )

Which may return something like this:

<table border="0" cellspacing="0" cellpadding="4">
  <tr>
    <th>
      Email
    </th>
    
    <th>
      NumberOfDuplicates
    </th>
  </tr>
  
  <tr>
    <td>
      joe@bloggs.com
    </td>
    
    <td>
      3
    </td>
  </tr>
  
  <tr>
    <td>
      spammer@spamilicious.com
    </td>
    
    <td>
      13
    </td>
  </tr>
  
  <tr>
    <td colspan="2">
      etc
    </td>
  </tr>
</table>

Now you can go about carefully resolving the duplicates, then adding the constraints to that column to prevent duplicates occurring again.