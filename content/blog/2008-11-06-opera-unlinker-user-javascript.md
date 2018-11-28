---
author: David
categories:
- Software Development
date: 2008-11-06T01:38:27Z
guid: http://davidmoore.info/?p=49
id: 49
tags:
- Applications
- javascript
- unlinker
- userjs
title: Opera "Unlinker" User JavaScript
url: /blog/2008/11/06/opera-unlinker-user-javascript/
aliases: /2008/11/06/opera-unlinker-user-javascript/
---

It's quite common on many websites, particularly forums, to post links to images.

Unlinker is a very popular plugin for Firefox, which allows you to change the links to images in the page to in-line images.

Opera doesn't have a fully-fledged plugin system like Firefox (which is a pro just as much as it is a con), but you can customize it using <a title="Opera User JavaScript" href="http://www.opera.com/support/tutorials/userjs/" target="_blank">User JavaScript</a>.

I've made a simple script to implement a very basic version of Unlinker. It will scan the page for links to images, and embed the image in the page under the link. It currently also scales the image down while maintaining aspect ratio if it exceeds 640&#215;480.

To use this, create a directory on your machine to store your user javascripts, and save the source there as unlinker.js (or whatever name you like).

  * Now in Opera, go to the Tools > Preferences menu
  * Go to the **Advanced** tab
  * Click the **Content** section
  * Click the **JavaScript Options&#8230;** button
  * Browse to the User JavaScript files folder where you saved the file, then hit OK
  * Hit OK
  * You don't have to restart Opera for the changes to take effect

The source code is:
  
`<br />
` 

    addEventListener(
          'load',
          function (e)
          {
              var isImageRegex = new RegExp(".gif|jpeg|jpg|png|bmp$", "i");
    
              var allAnchors = document.getElementsByTagName("a");
    
              for( var i = 0; i < allAnchors.length; i++ )
              {
                  var anchorElement = allAnchors[i];
                  var link = anchorElement.href;
                  if( link && isImageRegex.test(link) )
                  {
                      // The image tooltip will show the full image address
                      anchorElement.title = link;
    
                      // Create the image, giving it a border and some padding, resetting
                      // some styles and don't make it exceed 640x480 dimensions, auto-scaling it down
                      var image = document.createElement('IMG');
                      image.src = link;
                      image.style.border = 'solid 1px #ccc';
                      image.style.padding = '0px';
                      image.style.margin = '0px';
                      image.style.float = 'none';
                      image.style.maxWidth = '640px';
                      image.style.maxHeight = '480px';
    
                      anchorElement.appendChild( document.createElement('BR') );
                      anchorElement.appendChild(image);
                      anchorElement.appendChild( document.createElement('BR') );
                  }
              }
          },
          false
      );
    
    

`<strong>Edit 2010-05-29: Updated for Opera 10.x</strong><br />
`