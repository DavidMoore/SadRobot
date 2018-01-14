---
id: 409
title: Structuring Visual Studio solutions
date: 2011-01-22T23:12:44+00:00
author: David
guid: http://www.davidmoore.info/?page_id=409
---
The entire solution will be under a root folder, that may differ depending on the developer’s preferences, the branch they’re checking out etc.

## Branch structure

<table border="0" cellspacing="0" cellpadding="2" width="100%">
  <tr>
    <th valign="top" width="233">
      Folder Name</td>
    </th>
    
    <th valign="top" width="233">
      Function</td>
    </th>
    
    <th valign="top" width="233">
      Comments</td> </tr>
    </th>
  </tr>
  
  <tr>
    <td valign="top" width="233">
      Main
    </td>
    
    <td valign="top" width="233">
      Trunk / main branch
    </td>
    
    <td valign="top" width="233">
      &#160;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="233">
      Branches
    </td>
    
    <td valign="top" width="233">
      &#160;
    </td>
    
    <td valign="top" width="233">
      &#160;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="233">
      BranchesDevelopment
    </td>
    
    <td valign="top" width="233">
      Contains development branches
    </td>
    
    <td valign="top" width="233">
      &#160;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="233">
      BranchesReleases
    </td>
    
    <td valign="top" width="233">
      Contains live, maintenance branches
    </td>
    
    <td valign="top" width="233">
      &#160;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="233">
      General
    </td>
    
    <td valign="top" width="233">
      Non branch-specific resources
    </td>
    
    <td valign="top" width="233">
      E.g. Build server configuration, general documentation etc
    </td>
  </tr>
</table>

## Solution structure

<table border="0" cellspacing="0" cellpadding="2" width="100%">
  <tr>
    <th valign="top" width="304">
      Folder Name</td>
    </th>
    
    <th valign="top" width="295">
      Function</td>
    </th>
    
    <th valign="top" width="297">
      Comments</td> </tr>
    </th>
  </tr>
  
  <tr>
    <td valign="top" width="306">
      Bin
    </td>
    
    <td valign="top" width="294">
      Build drop location
    </td>
    
    <td valign="top" width="297">
      Drop location for binaries, making it easy to get to, and easy to reference from projects in separate solutions.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="308">
      Code
    </td>
    
    <td valign="top" width="293">
      Contains all projects
    </td>
    
    <td valign="top" width="296">
      Groups the code together instead of cluttering the root folder.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="309">
      Commons
    </td>
    
    <td valign="top" width="293">
      Contains shared project resources and non code
    </td>
    
    <td valign="top" width="296">
      Contains things such as build scripts, documentation, shared include files, strong name key, versioning scripts etc.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="310">
      CommonsLibraries
    </td>
    
    <td valign="top" width="293">
      Flat directory of binary libraries
    </td>
    
    <td valign="top" width="296">
      Contains managed and native assemblies referenced by any of the projects. Flat structure so that it’s easy to add references for, and use as a Reference Path.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="310">
      TestsUnitTests
    </td>
    
    <td valign="top" width="293">
      Contains Unit Test projects
    </td>
    
    <td valign="top" width="296">
      Tests that can and should be run regularly when developing, and added to increasingly through approaches such as TDD.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="310">
      TestsIntegrationTests
    </td>
    
    <td valign="top" width="293">
      Integration tests
    </td>
    
    <td valign="top" width="296">
      Integration tests that may require environment setup or more time, and won’t be run regularly during coding sessions, most regularly by continuous integration server.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="310">
      TestsHarnesses
    </td>
    
    <td valign="top" width="293">
      Test Harnesses
    </td>
    
    <td valign="top" width="296">
      Test harnesses to be used manually to test functions.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="310">
      <Solution>.sln
    </td>
    
    <td valign="top" width="293">
      Solution File
    </td>
    
    <td valign="top" width="297">
      The solution file exists in the root, where it’s easily accessible and can reach any and all contained folders and files.
    </td>
  </tr>
</table>