---
author: David
categories:
- .net
- Visual Studio
date: 2014-10-17T18:03:08Z
guid: http://www.davidmoore.info/blog/?p=1801
id: 1801
tags:
- lockscreen
- winrt
2014: "10"
title: 'Walkthrough: Using WinRT libraries from a Windows Desktop application'
description: 'These are the steps for enabling WinRT libraries from within your Windows Desktop application. A more detailed walkthrough and explanation follows.'
url: /blog/2014/10/17/walkthrough-using-winrt-libraries-from-a-windows-desktop-application/
aliases: /2014/10/17/walkthrough-using-winrt-libraries-from-a-windows-desktop-application/
toc: true
---

# Summary

These are the steps for enabling WinRT libraries from within your Windows Desktop application. A more detailed walkthrough and explanation follows.

## Steps

1) Editing your project file, add the platform target:

``` xml
  <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>
  <TargetPlatformVersion>8.0</TargetPlatformVersion>
</PropertyGroup>
```

2) Add the following references:

``` xml
  <Reference Include="Windows" />
  <Reference Include="System.Runtime" />
  <Reference Include="System.Runtime.InteropServices.WindowsRuntime" />
  <Reference Include="System.Runtime.WindowsRuntime" />
```

3) Load your project properties, and change the platform target from **AnyCPU** to **x64** (or **x86** if you're on a 32 bit operating system).

## Prerequisites / Limitations

  * You are obviously limited to WinRT-supported platforms: Windows 8 & 8.1, Windows Server 2012
  * Some of the WinRT libraries won’t work on the desktop platform, usually because they require a WinRT user interface. Pay attention to the MSDN docs which state whether they’re available for Desktop, but also feel free to experiment, as in some cases the docs are not accurate (for example, the Geolocation works on Desktop but the documentation states Windows Store apps only).

# Overview

You might be surprised to know that WinRT can be used from Windows apps also, with a little bit of tweaking.

## What is WinRT?

  * WinRT is not .NET or Win32, though it shares some similarities between both.
  * WinRT is an API over a new runtime, that supports platforms from Windows x86 to Windows Phone ARM.
  * WinRT is implemented in C++, but you can develop for it using C# and VB.NET.
  * Because the WinRT metadata is exposed as CLI metadata (in .WinMD files), you can reference and consume them from your CLR applications.

## Why would you want to use WinRT?

  * WinRT exposes some interesting APIs and libraries for things such as the accelerometer, web cam, geolocation, speech recognition and synthesis etc: <http://msdn.microsoft.com/en-us/library/windows/apps/br211377.aspx>

# Walk-through: Changing the Lock Screen

As a case study, we will look into changing the user lock screen to the Bing daily picture.

## Prerequisites

  * You will need to be reasonably comfortable with async code, as most of the API is exposed via Tasks.

## Getting started

Create a new Windows C# command line application:

![alt text](/wp-content/uploads/2014/10/clip_image0014.png "New console application")

I'll call mine **WinRTTest**.

## Referencing a WinRT library: Take 1

Now let's try adding a reference to a WinRT library.

Go to **Add Reference**, and choose **Browse**:

![](/wp-content/uploads/2014/10/clip_image0024.png "Add WinRT reference")

Then hit the **Browse** button, and select **C:\Program Files (x86)\Windows Kits\8.0\References\CommonConfiguration\Neutral\Windows.winmd** (or the 8.1 version) and click **OK**.

**CLANG!**

![](/wp-content/uploads/2014/10/clip_image0034.png)

Checking the documentation as instructed, we read this:

>   In the desktop projects, the Core subgroup doesn’t appear by default. You can add the Windows Runtime by opening the shortcut menu for the project node, <em>choosing Unload Project, adding the following snippet, and re-opening the project</em> (on the project node, choose Reload Project). When you invoke the Reference Manager dialog box, the Core subgroup appears.
> 
> ```xml
<PropertyGroup>
     <TargetPlatformVersion>8.0</TargetPlatformVersion>
</PropertyGroup>
```
> From http://msdn.microsoft.com/en-us/library/hh708954.aspx

Great! So now we know we must specify our target platform as 8.0.

## Preparing the Project File

First let's edit the project file; right click on the project file and choose Unload Project then Edit Project File.

I'll add the target platform property in the property group at the top of the project file:

```xml
<PropertyGroup>
  <Configuration Condition=" '$(Configuration)' == " ">Debug</Configuration> 
  <Platform Condition=" '$(Platform)' == " ">AnyCPU</Platform> 
  <ProjectGuid>{4725C47D-8877-47C8-BD56-134E656BFF09}</ProjectGuid> 
  <OutputType>Exe</OutputType> 
  <AppDesignerFolder>Properties</AppDesignerFolder> 
  <RootNamespace>WinRTTest</RootNamespace> 
  <AssemblyName>WinRTTest</AssemblyName> 
  <TargetFrameworkVersion>v4.5.1</TargetFrameworkVersion> 
  <FileAlignment>512</FileAlignment> 
  <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects> 
  <TargetPlatformVersion>8.0</TargetPlatformVersion><!-- Add this property -->
</PropertyGroup>
```

## Referencing a WinRT Library: Take 2

Now reload the project and choose **Add Reference&#8230;** again. Suddenly, the Windows tab is available for us:

![](/wp-content/uploads/2014/10/clip_image0064.png)

Let's tick **Windows** and click **OK**.

Now let's start coding with the WinRT libraries.

## Adding the HttpClient NuGet package for downloading the Bing picture

The HttpClient class will be a nice easy way for us to use the Bing Daily Picture service.

First, add a reference to the NuGet package for the HttpClient.

  1. In the Visual Studio menu, go to **Tools** > **NuGet Package Manager** > **Package Manager Console**
  2. Then type in the following command at the prompt:**Install-Package Microsoft.AspNet.WebApi.Client**

```
Install-Package Microsoft.AspNet.WebApi.Client
Attempting to resolve dependency 'Newtonsoft.Json (≥ 6.0.4)'.
Installing 'Newtonsoft.Json 6.0.4'.
Successfully installed 'Newtonsoft.Json 6.0.4'.
Installing 'Microsoft.AspNet.WebApi.Client 5.2.2'.
You are downloading Microsoft.AspNet.WebApi.Client from Microsoft, the license agreement to which is available at <a href="http://www.microsoft.com/web/webpi/eula/net_library_eula_ENU.htm">http://www.microsoft.com/web/webpi/eula/net_library_eula_ENU.htm</a>. Check the package for additional dependencies, which may come with their own license agreement(s). Your use of the package and dependencies constitutes your acceptance of their license agreements. If you do not accept the license agreement(s), then delete the relevant components from your device.
Successfully installed 'Microsoft.AspNet.WebApi.Client 5.2.2'.
Adding 'Newtonsoft.Json 6.0.4' to WinRTTest.
Successfully added 'Newtonsoft.Json 6.0.4' to WinRTTest.
Adding 'Microsoft.AspNet.WebApi.Client 5.2.2' to WinRTTest.
Successfully added 'Microsoft.AspNet.WebApi.Client 5.2.2' to WinRTTest.
```

So now we have our new references:

![](http://www.davidmoore.info/blog/wp-content/uploads/2014/10/clip_image0084.png)

## The Code

Now, paste in the code below:

&nbsp;



> Note that we are hard-coded to get the 1080p version of the desktop, and there's not much error handling. We're keeping it nice and brief; getting the appropriate wallpaper size and error handling could be left as a future exercise.

## David, your code sucks. It won’t compile.

I can’t argue with those statements:
```
1>------ Build started: Project: WinRTTest, Configuration: Debug Any CPU ------
1>C:\Projects\WinRTTest\WinRTTest\Program.cs(37,32,37,168): error CS4028: 'await' requires that the type 'Windows.Foundation.IAsyncOperation<Windows.Storage.StorageFile>' have a suitable GetAwaiter method. Are you missing a using directive for 'System'?
========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ==========
```

If you paid close attention to the MSDN docs earlier, it referred us to another page which states:

> That said, _your desktop app can’t consume much of anything from the Windows Runtime until you prepare your project with one essential reference_. The Windows Runtime defines some standard classes and interfaces in System.Runtime, such as IEnumerable, that are used throughout the Windows Runtime libraries. By default, your managed desktop app won’t be able to find these types, and so **you must manually reference System.Runtime** before you can do anything meaningful with Windows Runtime classes.
> 
> From http://msdn.microsoft.com/en-us/library/windows/apps/jj856306.aspx#consuming_standard_windows_runtime_types

While we could browse around for files, I believe it's actually less error prone and simpler to reference the assembly name in our project file, and let Visual Studio do the rest. It also means you can prepare your project for WinRT in one edit of the project file (see the summary at the top of the article).

Now the System.Runtime reference isn't going to be enough for us, as the async support extensions are in the WindowsRuntime classes. So add the following:

```xml
  <Reference Include="Windows" />
  <Reference Include="System.Runtime" /><!-- Added reference -->
  <Reference Include="System.Runtime.InteropServices.WindowsRuntime" /><!-- Added reference -->
  <Reference Include="System.Runtime.WindowsRuntime" /><!-- Added reference -->
</ItemGroup>
```

Now we can compile!

# Testing

So we run the app. The image comes down and is saved into our Pictures folder as LockScreen.jpg:

![](/wp-content/uploads/2014/10/clip_image0094.png)

But if you lock your machine by hitting **Windows + L**, our lock screen isn't showing the changes.

Weirdly, it's showing in the control panel though:

![](/wp-content/uploads/2014/10/clip_image0104.png)

Well after some trial and error myself, let's change the target platform from **AnyCPU** to **x64** (or **x86** if you're on a 32 bit machine):

![](/wp-content/uploads/2014/10/clip_image0114.png)

And it _should_ suddenly work!

> Now, it's unclear why this is necessary (and why we see no errors, and the lock screen actually shows in the control panel). Frustratingly, I can't troubleshoot the problem properly, as setting the platform target back to Any CPU suddenly continues to work also. There may be something else happening here; so I will update this article if an explanation ever comes to light.

# Conclusion

Now you can play around with some of the interesting WinRT libraries from your desktop applications, as well as exciting new WinRT extensions such as the Microsoft OCR Library: http://blogs.windows.com/buildingapps/2014/09/18/microsoft-ocr-library-for-windows-runtime/