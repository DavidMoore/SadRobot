---
author: David
categories:
- .net
- How To
- Software Development
date: 2009-05-21T16:53:17Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=138
id: 138
tags:
- bindings
- project
- root
- solution
- source control
- visual studio
- vs
title: 'Visual Studio: Cannot add project to source control; it overlaps a project
  that is already bound to source control at a lower root'
url: /blog/2009/05/21/visual-studio-cannot-add-project-to-source-control-it-overlaps-a-project-that-is-already-bound-to-source-control-at-a-lower-root/
aliases: /2009/05/21/visual-studio-cannot-add-project-to-source-control-it-overlaps-a-project-that-is-already-bound-to-source-control-at-a-lower-root/
---

I've been getting this error a bit lately as I trying to add new projects to the solution, and then add them to source control: <blockquote>The project <ProjectName> cannot be added to source control. In folder <SolutionDir>, it overlaps a project that is already bound to source control at a lower root. To avoid this problem, add the project from a location below the binding root of the other source controlled projects in the solution.</blockquote> The cause of this was that I had linked files within the new project that were pointing to existing files higher up in the solution folder (in this instance, in the solution root). In this case I was linking to the strong name key from the solution root: <SolutionRoot>MyKey.snk <SolutionRoot>MyProjectMyProject.csproj <= Was linking to the key in the root To add the project to source control, you have to remove these links first, add the project to source control, then you can put your links back in.