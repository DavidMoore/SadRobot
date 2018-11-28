---
author: David
categories:
- C++
date: 2013-05-27T13:26:20Z
guid: http://www.sadrobot.co.nz/?p=641
id: 641
tags:
- visual studio
title: "Error C2039: 'SetDefaultDllDirectories' when targetting Visual Studio 2012 Windows XP C++ Runtime"
url: /blog/2013/05/27/error-c2039-setdefaultdlldirectories-when-targetting-visual-studio-2012-windows-xp-c-runtime/
aliases: /2013/05/27/error-c2039-setdefaultdlldirectories-when-targetting-visual-studio-2012-windows-xp-c-runtime/
---

We’re switching our legacy C++ projects from Visual C++ 2010 to the Visual C++ 2012 Runtime, now that Microsoft allows you to <a href="http://blogs.msdn.com/b/vcblog/archive/2012/10/08/10357555.aspx" target="_blank">target Windows XP for C++ in 2012</a> (available in Visual Studio Update 1).

So that involves switching the Platform Target from v100:

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image_thumb.png" width="856" height="609" />](http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image.png)

To v110_xp:

[<img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image_thumb1.png" width="613" height="41" />](http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image1.png)

Well upon compilation, I saw these errors for one particular project:

[<img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image_thumb2.png" width="686" height="90" />](http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image2.png)

The key error being **Error C2039: 'SetDefaultDllDirectories' : is not a member of '\`global namespace"** from line **638** in **atlcore.h**

Well if we jump into that code, we see this:

<pre>#ifndef _USING_V110_SDK71_
	// the LOAD_LIBRARY_SEARCH_SYSTEM32 flag for LoadLibraryExW is only supported if the DLL-preload fixes are installed, so
	// use LoadLibraryExW only if SetDefaultDllDirectories is available (only on Win8, or with KB2533623 on Vista and Win7)...
	IFDYNAMICGETCACHEDFUNCTION(L"kernel32.dll", SetDefaultDllDirectories, pfSetDefaultDllDirectories)
	{
		return(::LoadLibraryExW(pszLibrary, NULL, LOAD_LIBRARY_SEARCH_SYSTEM32));
	}
#endif</pre>

It looks like that define **should** exist, as we’re targeting “V110\_SDK71” (aka v110\_xp).

Well, with a little digging, that define is getting created by the C++ MSBuild files in **C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V110\Platforms\Win32\PlatformToolsets\v110\_xp\Microsoft.Cpp.Win32.v110\_xp.props**:

<pre>&nbsp; &lt;ItemDefinitionGroup&gt;<br />&nbsp;&nbsp;&nbsp; &lt;ClCompile&gt;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;!-- Add /D_USING_V110_SDK71_ when targeting XP --&gt;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;PreprocessorDefinitions&gt;_USING_V110_SDK71_;%(PreprocessorDefinitions)&lt;/PreprocessorDefinitions&gt;<br />&nbsp;&nbsp;&nbsp; &lt;/ClCompile&gt;</pre>

But was getting blown away in my project file:

<pre>&nbsp; &lt;ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'"&gt;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ClCompile&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;RuntimeLibrary&gt;MultiThreadedDLL&lt;/RuntimeLibrary&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;InlineFunctionExpansion&gt;OnlyExplicitInline&lt;/InlineFunctionExpansion&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;StringPooling&gt;true&lt;/StringPooling&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;FunctionLevelLinking&gt;true&lt;/FunctionLevelLinking&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Optimization&gt;MinSpace&lt;/Optimization&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;SuppressStartupBanner&gt;true&lt;/SuppressStartupBanner&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;WarningLevel&gt;Level3&lt;/WarningLevel&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font style="background-color: #ffff00">&lt;PreprocessorDefinitions&gt;&lt;/PreprocessorDefinitions&gt;</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;AssemblerListingLocation&gt;$(IntDir)&lt;/AssemblerListingLocation&gt;</pre>

So the fix is to include any existing pre-processor definitions (i.e. the Microsoft one) before defining our own (don’t forget to do this for all configurations and platforms in your project file):

<pre>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;WarningLevel&gt;Level3&lt;/WarningLevel&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;PreprocessorDefinitions&gt;<font style="background-color: #ffff00">%(PreprocessorDefinitions)</font>&lt;/PreprocessorDefinitions&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;AssemblerListingLocation&gt;$(IntDir)&lt;/AssemblerListingLocation&gt;</pre>

Otherwise, you can simply remove the PreprocessorDefinition element itself (if you have no defines of your own), or choose to inherit from the parent or project defaults from the project properties (which will essentially do the same thing):

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image_thumb3.png" width="697" height="233" />](http://www.sadrobot.co.nz/wp-content/uploads/2013/05/image3.png)

And now we recompile fine.