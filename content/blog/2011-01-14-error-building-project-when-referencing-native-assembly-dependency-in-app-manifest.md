---
author: David
categories:
- .net
- How To
- Software Development
date: 2011-01-14T08:45:38Z
guid: http://www.davidmoore.info/?p=404
id: 404
tags:
- manifest
- sxs
title: Error building project when referencing native assembly dependency in app.manifest
url: /blog/2011/01/14/error-building-project-when-referencing-native-assembly-dependency-in-app-manifest/
aliases: /2011/01/14/error-building-project-when-referencing-native-assembly-dependency-in-app-manifest/
---

If you're using an app.manifest, and defining assembly dependencies (i.e. for SxS / Side by side / Reg-free COM etc), you may encounter this error when you build the project:

<p style="padding-left: 30px;">
  <span style="color: #ff0000;">Could not find file 'AssemblyName, Version=x.x.x.x, PublicKeyToken=xxxxxxxxxxx, ProcessorArchitecture=x86, Type=win32&#8242;.</span>
</p>

This is even when the native assembly is in place where the project can find it.

## Example

For example, your **app.manifest** may contain this fragment:

<p class="MsoNormal" style="tab-stops: 45.8pt 91.6pt 137.4pt 183.2pt 229.0pt 274.8pt 320.6pt 366.4pt 412.2pt 458.0pt 503.8pt 549.6pt 595.4pt 641.2pt 687.0pt 732.8pt;">
  <span style="font-size: 10.0pt; font-family: Consolas; mso-fareast-font-family: &quot;Times New Roman&quot;; color: blue; mso-fareast-language: EN-NZ;"><</span><span style="font-size: 10.0pt; font-family: Consolas; mso-fareast-font-family: &quot;Times New Roman&quot;; color: #a31515; mso-fareast-language: EN-NZ;">dependency</span><span style="font-size: 10.0pt; font-family: Consolas; mso-fareast-font-family: &quot;Times New Roman&quot;; color: blue; mso-fareast-language: EN-NZ;">></span><span style="font-size: 10.0pt; font-family: Consolas; mso-fareast-font-family: &quot;Times New Roman&quot;; mso-fareast-language: EN-NZ;"><br /> <span style="color: blue;"> <</span><span style="color: #a31515;">dependentAssembly</span><span style="color: blue;">></span><br /> <span style="color: blue;"> <</span><span style="color: #a31515;">assemblyIdentity</span><span style="color: blue;"> </span><span style="color: red;">name</span><span style="color: blue;">=</span>"<span style="color: blue;">Native.Custom</span>"<span style="color: blue;"> </span><span style="color: red;">version</span><span style="color: blue;">=</span>"<span style="color: blue;">1.0.0.0</span>"<span style="color: blue;"> </span><span style="color: red;">processorArchitecture</span><span style="color: blue;">=</span>"<span style="color: blue;">x86</span>"<span style="color: blue;"> </span><span style="color: red;">type</span><span style="color: blue;">=</span>"<span style="color: blue;">win32</span>"<span style="color: blue;"> </span><span style="color: red;">publicKeyToken</span><span style="color: blue;">=</span>"<span style="color: blue;">12345678</span>"<span style="color: blue;">/></span><br /> <span style="color: blue;"> </</span><span style="color: #a31515;">dependentAssembly</span><span style="color: blue;">></span><br /> <span style="color: blue;"> </</span><span style="color: #a31515;">dependency</span><span style="color: blue;">></span></span>
</p>

This manifest is available to the project, with the manifest file in the project directory or in a subdirectory called "Native.Custom".

In this case, I have a sub directory called Native.Custom, which contains my Native.Custom.manifest file.

## Solution

The problem may be because the ClickOnce manifests are being generated.

  1. Open your project file in a text editor (or right click it in Visual Studio and choose **Edit Project**)
  2. Find the � **GenerateManifests** element and set it to false:
  3. <span style="color: blue;"><</span><span style="color: #a31515;">GenerateManifests</span><span style="color: blue;">></span>false<span style="color: blue;"></</span><span style="color: #a31515;">GenerateManifests</span><span style="color: blue;">></span>
  4. Save the project and reload it.

Now you should hopefully be able to build.