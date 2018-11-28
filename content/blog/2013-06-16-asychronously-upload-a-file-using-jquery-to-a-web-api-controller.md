---
author: David
categories:
- Uncategorized
date: 2013-06-16T20:30:35Z
guid: http://www.sadrobot.co.nz/?p=691
id: 691
title: Asychronously upload a file using jQuery to a Web API controller
url: /blog/2013/06/16/asychronously-upload-a-file-using-jquery-to-a-web-api-controller/
aliases: /2013/06/16/asychronously-upload-a-file-using-jquery-to-a-web-api-controller/
---

Here’s the code for the HTML5 form:

{{< highlight html >}}
<pre><code class="language-markup">&lt;form id="upload"&gt;
    &lt;div&gt;
        &lt;label for="myFile"&gt;&lt;/label&gt;
        &lt;div&gt;
            &lt;input type="file" id="myFile" /&gt;
        &lt;/div&gt;
    &lt;/div&gt;
    &lt;button type="submit"&gt;Upload&lt;/button&gt;
&lt;/form&gt;</code></pre>
{{< /highlight >}}

We need to use jQuery to handle when the user submits the upload, to make sure it gets handled asynchronously and posted to our Web API controller:
  

{{< highlight javascript >}}
// Hook into the form's submit event.
$('#upload').submit(function () {

    // To keep things simple in this example, we'll
    // use the FormData XMLHttpRequest Level 2 object (which
    // requires modern browsers e.g. IE10+, Firefox 4+, Chrome 7+, Opera 12+ etc).
    var formData = new FormData();

    // We'll grab our file upload form element (there's only one, hence [0]).
    var opmlFile = $('#opmlFile')[0];

    // If this example we'll just grab the one file (and hope there's at least one).
    formData.append("opmlFile", opmlFile.files[0]);

    // Now we can send our upload!
    $.ajax({
        url: 'api/upload', // We'll send to our Web API UploadController
        data: formData, // Pass through our fancy form data

        // To prevent jQuery from trying to do clever things with our post which
        // will break our upload, we'll set the following to false
        cache: false,
        contentType: false,
        processData: false,

        // We're doing a post, obviously.
        type: 'POST',

        success: function () {
            // Success!
            alert('Woot!');
        }
    });

    // Returning false will prevent the event from
    // bubbling and re-posting the form (synchronously).
    return false;
});
{{< /highlight >}}
  
Ok and now in our controller, we can deal with the uploaded file(s):

<pre><code class="language-csharp">    using System;
    using System.IO;
    using System.Net;
    using System.Net.Http;
    using System.Web;
    using System.Web.Http;

    class UploadController : ApiController
    {
        public async void Post()
        {
            if (!Request.Content.IsMimeMultipartContent())
            {
                throw new HttpResponseException(Request.CreateResponse(HttpStatusCode.NotAcceptable, "This request is not properly formatted"));
            }

            // We'll store the uploaded files in an Uploads folder under the web app's App_Data special folder
            var streamProvider = new MultipartFormDataStreamProvider(HttpContext.Current.Server.MapPath("~/App_Data/Uploads/"));

            // Once the files have been written out, we can then process them.
            await Request.Content.ReadAsMultipartAsync(streamProvider).ContinueWith(t =&gt;
            {
                if (t.IsFaulted || t.IsCanceled)
                {
                    throw new HttpResponseException(HttpStatusCode.InternalServerError);
                }

                // Here we can iterate over each file that got uploaded.
                foreach (var fileData in t.Result.FileData)
                {
                    // Some good things to do are to check the MIME type before we do the processing, e.g. for XML:
                    if (fileData.Headers.ContentType.MediaType.Equals("text/xml", StringComparison.InvariantCultureIgnoreCase))
                    {
                        // And this is how we can read the contents (note you would probably want to do this asychronously
                        // but let's try keep things simple for now).
                        string contents = File.ReadAllText(fileData.LocalFileName);
                    }
                }
            });
        }
    }</code></pre>