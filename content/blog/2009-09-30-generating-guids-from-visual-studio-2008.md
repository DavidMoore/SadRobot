---
author: David
categories:
- .net
- How To
date: 2009-09-30T12:03:22Z
excerpt: |2

  <![CDATA[]]>
guid: http://www.davidmoore.info/?p=223
id: 223
tags:
- "2008"
- guid
- macro
- new
- paste
- visual studio
- vs
- vs.net
title: Generating GUIDs from Visual Studio 2008
url: /blog/2009/09/30/generating-guids-from-visual-studio-2008/
aliases: /2009/09/30/generating-guids-from-visual-studio-2008/
---

I find I have to generate GUIDs often (mostly due to using WiX) and the in-built <strong>Tools</strong> > <strong>Create GUID</strong> tool is too cumbersome for this. I found a blog post that has a simple macro you can customize to bind a keyboard shortcut to <a href="http://www.wirwar.com/blog/2007/11/03/generating-guids-in-the-visual-studio-ide/" target="_blank">paste in a new GUID</a> Here are some full instructions, using their simple macro code: <ol> <li><strong>Tools</strong> > <strong>Macros</strong> > <strong>Macro Explorer</strong> (or hit <strong>ALT</strong>+<strong>F8</strong>)</li> <li>Right click <strong>Macros</strong>, choose <strong>New Macro Project&#8230;</strong></li> <li>Choose a location for the Macro project and give it a meaningful name then click <strong>Add</strong></li> <li>Rename Module1 to something more meaningful, then double-click to edit the module</li> <li>Insert the code to paste a new GUID into the current cursor position / selection: <code> Public Sub PasteNewGuid() DTE.ActiveDocument.Selection.Text = "{" & System.Guid.NewGuid().ToString("D").ToUpper() & "}" End Sub</code></li> <li>Save the macro project and close the Macro IDE</li> <li>In Visual Studio: <strong>Tools</strong> > <strong>Options</strong>, select <strong>Environment</strong> > <strong>Keyboard</strong></li> <li>Find the macro command you created (you can use the Show commands containing: to search on guid)</li> <li>Select the command in the list</li> <li>Ensure <strong>Use new shortcut in:</strong> has <strong>Global</strong> selected</li> <li>Place the cursor in <strong>Press shortcut keys:</strong> and hit the shortcut (<strong>ALT</strong>+<strong>G</strong> for me)</li> <li>Hit <strong>OK</strong></li> <li>Test it out</li> </ol>