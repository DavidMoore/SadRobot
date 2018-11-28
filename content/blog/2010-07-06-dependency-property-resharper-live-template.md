---
author: David
categories:
- .net
date: 2010-07-06T22:30:00Z
guid: http://www.davidmoore.info/2010/07/06/dependency-property-resharper-live-template/
id: 368
tags:
- Dependency Property
- Live Template
- ReSharper
title: Dependency Property ReSharper Live Template
url: /blog/2010/07/06/dependency-property-resharper-live-template/
aliases: /2010/07/06/dependency-property-resharper-live-template/
---

[Dependency Property ReSharper Live Template](http://www.sadrobot.co.nz/wp-content/uploads/2010/07/DependencyPropertyLiveTemplate.zip)

Don’t you love Dependency Properties?

After the ease of automatic properties though, dependency properties are a chore to define.

If you’ve got ReSharper (if not, why not?), I’ve got a simple Live Template you can use to create your dependency properties.

I’ve set it up to use the dp keyword.

Here it is in use. Typing dp first to pop up the template:

[<img class="wlDisabledImage" style="margin: 0px; display: inline; border-width: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image.png" border="0" alt="image" />](http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image.png)

Hitting **tab** or **enter** will run the template, with the name macro already selected:

[<img class="wlDisabledImage" style="margin: 0px; display: inline; border-width: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image1.png" border="0" alt="image" />](http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image1.png)

Type in the name of the property. This will set up the wrapper property with that name, and the dependency property’s name will be the name you chose, with “Property” added to the end.

For example, I type in MyCaption as the property name:

[<img class="wlDisabledImage" style="margin: 0px; display: inline; border-width: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image2.png" border="0" alt="image" />](http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image2.png)

Hitting tab shifts me to the next macro, which is the **type** for the dependency property:

[<img class="wlDisabledImage" style="display: inline; border-width: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image3.png" border="0" alt="image" />](http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image3.png)

My property will be of type **string**, so typing that in will bring up string in the suggestions. Hitting **tab** will select this; hitting **tab** again will confirm this as my type, and select the next and last macro, the owner type:

[<img class="wlDisabledImage" style="margin: 0px; display: inline; border-width: 0px;" title="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image4.png" border="0" alt="image" />](http://www.sadrobot.co.nz/wp-content/uploads/2010/07/image4.png)

This will automatically be set to the name of the containing type anyway, so you can normally leave this as is; hit **tab** one more time and you’re done.