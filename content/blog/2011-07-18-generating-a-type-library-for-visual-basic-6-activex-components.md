---
author: David
categories:
- Entertainment
date: 2011-07-18T14:12:27Z
guid: http://www.davidmoore.info/2011/07/18/generating-a-type-library-for-visual-basic-6-activex-components/
id: 430
title: Generating a type library for Visual Basic 6 ActiveX Components
url: /blog/2011/07/18/generating-a-type-library-for-visual-basic-6-activex-components/
aliases: /2011/07/18/generating-a-type-library-for-visual-basic-6-activex-components/
---

When generating setup code or isolation code (for Side by Side assemblies and Registration-free COM), VB6 ActiveX Components can be a little troublesome.

ActiveX exes in particular can be difficult, with the WiX heat tool and various SxS tools not being able to harvest COM registration information from them properly.

A good way of avoiding these problems is to generate a type library (.tlb) from the VB6 component, and then pointing the code generation tools at the type library.

In VB6, you can generate a Type Library (.tlb) file for an ActiveX component:

  1. **Project** > **<Project Name> Properties…**
  2. Go to the **Component** tab
  3. Check **Remote Server Files**
  4. Click **OK** and build the project

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2011/07/image_thumb.png" width="234" height="244" />](http://www.sadrobot.co.nz/wp-content/uploads/2011/07/image.png)

You should now see a **.tlb** and **.vbr** file next to your binary.

The .vbr file is a text file containing registry information, which will be very helpful if the type library is still missing information you want to use for your isolation or installation authoring.

## Reference

[How To Make a Typelib (.TLB) File for ActiveX Components @ MSDN](http://support.microsoft.com/kb/161272)