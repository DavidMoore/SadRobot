---
author: David
categories:
- How To
- Software Development
date: 2009-02-07T02:17:03Z
excerpt: |2
guid: http://davidmoore.info/?p=76
id: 76
tags:
- .net
- c#
- crop
- image
- resize
- thumb
- thumbnail
title: Creating thumbnail images with automatic cropping and maintaining aspect ratio
url: /blog/2009/02/07/creating-thumbnail-images-with-automatic-cropping-and-maintaining-aspect-ratio/
aliases: /2009/02/07/creating-thumbnail-images-with-automatic-cropping-and-maintaining-aspect-ratio/
---

 Most thumbnail-generation solutions will shrink the original down while maintaining aspect ratio.

 Usually you specify the maximum height and width of the thumbnail, e.g. 150 x 200

 However, if your original image's aspect ratio is different to the maximum thumbnail dimensions, you will end up with dead space vertically or horizontally (shown in green in the illustration). This can be quite an eyesore when displaying thumbnails in a grid. 

<img class="alignnone size-full wp-image-77" title="Normal Thumbnail Resizing Diagram" src="http://davidmoore.info/wp-content/uploads/2009/02/image-resize-normal.gif" alt="Normal Thumbnail Resizing Diagram" width="672" height="334" />

I've got an algorithm that will automatically crop the image either horizontally or vertically to then match the thumbnail aspect ratio, so you end up with the thumbnails all being the same size even though they may be coming from originals of wildly different aspect ratio.

<!--more--> 

In the illustration, you can see that the image is scaled down and fills all the available thumbnail space, showing the parts in grey from the original that were cropped out.

<img class="alignnone size-full wp-image-78" title="Image resizing with automatic cropping" src="http://davidmoore.info/wp-content/uploads/2009/02/image-resize-crop.gif" alt="Image resizing with automatic cropping" width="716" height="333" /> 

The algorithm does the cropping before the resizing. It takes the width and height of the original image, and the width and height of the desired thumbnail. It will return the width and height that the original must be cropped to, to match the aspect ratio of the thumbnail.

<img class="alignnone size-full wp-image-79" title="Image resize with automatic cropping C# code" src="http://davidmoore.info/wp-content/uploads/2009/02/image-resize-crop.png" alt="Image resize with automatic cropping C# code" width="926" height="521" /> 

Of course this isn't quite enough; where do we do the cropping? All from the top of the image, or the bottom, or a mix? Ideally we want the user to choose which parts of the original they want cropped out. But we can do some very simple automatic cropping by cropping equal amounts from each side that needs to be cropped. 

<img class="alignnone size-full wp-image-80" title="image-resize-crop-rectangle" src="http://davidmoore.info/wp-content/uploads/2009/02/image-resize-crop-rectangle.png" alt="image-resize-crop-rectangle" width="950" height="229" />

 Now we know exactly which part of the original we can take and then resize down to a thumbnail.