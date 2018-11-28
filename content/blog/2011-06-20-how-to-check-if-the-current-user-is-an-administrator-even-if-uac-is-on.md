---
author: David
categories:
- Entertainment
date: 2011-06-20T11:23:47Z
guid: http://www.davidmoore.info/2011/06/20/how-to-check-if-the-current-user-is-an-administrator-even-if-uac-is-on/
id: 415
title: How to check if the current user is an Administrator (even if UAC is on)
url: /blog/2011/06/20/how-to-check-if-the-current-user-is-an-administrator-even-if-uac-is-on/
aliases: /2011/06/20/how-to-check-if-the-current-user-is-an-administrator-even-if-uac-is-on/
---

There may be a scenario where you want to determine from code if the current user is an Administrator.

One example of this which I have had to deal with is checking for software updates.

Say your application contacts a service to see if there is a newer version of the application available; if so, you can download and run the installer.

Imagine that the installer requires admin privileges; you don’t want to run the installer if the current user does not have administrative privileges.

So how can we check if the user is an admin or not?

## In VB6, C++ etc

There is a Windows API function you can use very easily to see if the current user is an admin: [IsUserAnAdmin](http://msdn.microsoft.com/en-us/library/bb776463(v=vs.85).aspx).

> BOOL IsUserAnAdmin(void);

### Visual Basic 6 Declaration

> <span style="font-family: &amp;quot;"><span style="line-height: 12pt;"><span style="color: #00007f;"><span style="font-size: 10pt;">Private</span></span></span><span style="font-size: 10pt;"><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Declare</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Function</span></span><span style="line-height: 12pt;"> IsUserAnAdmin </span><span style="line-height: 12pt;"><span style="color: #00007f;">Lib</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #7f007f;">"Shell32&#8243;</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Alias</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #7f007f;">"#680&#8243;</span></span><span style="line-height: 12pt;"> () </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> </span></span><span style="line-height: 12pt;"><span style="font-size: 10pt; color: #00007f;">Integer</span></span></span>

While you can still use this, it is actually deprecated, and the documentation recommends you call the [CheckTokenMembership](http://msdn.microsoft.com/en-us/library/aa376389(v=vs.85).aspx) function instead (which IsUserAnAdmin is a wrapper for).

## .NET

### C#.NET

<span style="font-family: &amp;quot;"><strong><span><span style="color: #859900;">using</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">System</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;<br /> </span></strong></span><span style="font-family: &amp;quot;"><strong><span><span style="color: #859900;">using</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">System</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #00008b;">Security</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #00008b;">Principal</span></span><span style="color: #586e75;">;</span></strong></span>

<pre style="padding-bottom: 0px; line-height: normal; width: auto; background: #fdf6e3; overflow: visible;"><span style="font-family: &amp;quot;"><strong><span><span style="color: #859900;">var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">identity</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">WindowsIdentity</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">GetCurrent</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">();
</span><span><span style="color: #859900;">if</span></span><span style="color: #586e75;"> (</span><span><span style="color: #657b83;">identity</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">==</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">null</span></span><span style="color: #586e75;">) </span><span><span style="color: #859900;">throw</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">new</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">InvalidOperationException</span></span><span style="color: #586e75;">(</span><span><span style="color: #2aa198;">"Couldn't get the current user identity"</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);
</span><span><span style="color: #859900;">var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">principal</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">new</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">WindowsPrincipal</span></span><span style="color: #586e75;">(</span><span><span style="color: #657b83;">identity</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);</span>
<span><span style="color: #859900;">return</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">principal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">IsInRole</span></span><span style="color: #586e75;">(</span><span><span style="color: #00008b;">WindowsBuiltInRole</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Administrator</span></span><span style="color: #586e75;">)</span><span style="color: #586e75;">;</span></strong></span></pre>

## User Account Control (UAC)

A problem arises when you use any of the above code on a machine that has UAC enabled, and the process is not elevated.

While the user may be an administrator, when the process is not elevated yet, the user has a split token &#8211; which doesn’t have the administrator privileges.

A way around this is to use the [GetTokenInformation](http://msdn.microsoft.com/en-us/library/aa446671(v=VS.85).aspx) API call to inspect the token to see if it’s a split token. In _most_ cases this will mean that UAC is on and the current user is an administrator.

_This is not 100% reliable_ (see References) but it’s probably the best we can do for now.

### C#.NET

This code is slightly easier in .NET, as there’s already a fair amount of code we don’t have to write to get the current process’s token.

First, we’ll need some code to support the GetTokenInformation API call:

<pre style="padding-bottom: 0px; line-height: normal; width: auto; background: #fdf6e3; overflow: visible;"><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">[</span><span><span style="color: #00008b;">DllImport</span></span><span style="color: #586e75;">(</span><span><span style="color: #2aa198;">"advapi32.dll"</span></span><span style="color: #586e75;">, </span><span><span style="color: #800080;">SetLastError</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">true</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">)]
</span><span><span style="color: #859900;">static</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">extern</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">bool</span></span><span style="color: #586e75;"> </span><span><span style="color: #008b8b;">GetTokenInformation</span></span><span style="color: #586e75;">(</span><span><span style="color: #00008b;">IntPtr</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">tokenHandle</span></span><span style="color: #586e75;">, </span><span><span style="color: #00008b;">TokenInformationClass</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">tokenInformationClass</span></span><span style="color: #586e75;">, </span><span><span style="color: #00008b;">IntPtr</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">tokenInformation</span></span><span style="color: #586e75;">, </span><span><span style="color: #859900;">int</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">tokenInformationLength</span></span><span style="color: #586e75;">, </span><span><span style="color: #859900;">out</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">int</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">returnLength</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);

</span><span style="color: #93a1a1;"><span style="background-color: #eee8d5;"><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">///</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> </span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">&lt;summary&gt;</span></span></span>
<span style="color: #93a1a1;"><span style="background-color: #eee8d5;"><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">///</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> Passed to </span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">&lt;see cref=</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">"GetTokenInformation"</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">/&gt;</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> to specify what</span></span></span>
<span style="color: #93a1a1;"><span style="background-color: #eee8d5;"><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">///</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> information about the token to return.</span></span></span>
<span style="color: #93a1a1;"><span style="background-color: #eee8d5;"><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">///</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> </span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">&lt;/summary&gt;</span></span></span>
<span><span style="color: #859900;">enum</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">TokenInformationClass</span></span>
</strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">{
     </span><span><span style="color: #800080;">TokenUser</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #2aa198;">1</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenGroups</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenPrivileges</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenOwner</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenPrimaryGroup</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenDefaultDacl</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenSource</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenType</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenImpersonationLevel</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenStatistics</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenRestrictedSids</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenSessionId</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenGroupsAndPrivileges</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenSessionReference</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenSandBoxInert</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenAuditPolicy</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenOrigin</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenElevationType</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenLinkedToken</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenElevation</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenHasRestrictions</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenAccessInformation</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenVirtualizationAllowed</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenVirtualizationEnabled</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenIntegrityLevel</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenUiAccess</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenMandatoryPolicy</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">TokenLogonSid</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
     </span><span><span style="color: #800080;">MaxTokenInfoClass</span></span>
</strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">}

</span><span style="color: #93a1a1;"><span style="background-color: #eee8d5;"><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">///</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> </span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">&lt;summary&gt;</span></span></span>
<span style="color: #93a1a1;"><span style="background-color: #eee8d5;"><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">///</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> The elevation type for a user token.</span></span></span>
<span style="color: #93a1a1;"><span style="background-color: #eee8d5;"><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">///</span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;"> </span><span style="background-image: none; background-attachment: scroll; background-repeat: repeat; background-position: 0% 0%;">&lt;/summary&gt;</span></span></span>
<span><span style="color: #859900;">enum</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">TokenElevationType</span></span>
</strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">{
    </span><span><span style="color: #800080;">TokenElevationTypeDefault</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #2aa198;">1</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
    </span><span><span style="color: #800080;">TokenElevationTypeFull</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">,
    </span><span><span style="color: #800080;">TokenElevationTypeLimited</span></span>
<span style="color: #586e75;">}</span></strong></span></pre>

<span style="font-family: &amp;quot;"><strong><span><span style="color: #859900;"> </span></span></strong></span>

Then, the actual code to detect if the user is an Administrator (returning true if they are, otherwise false).

<pre style="padding-bottom: 0px; line-height: normal; width: auto; background: #fdf6e3; overflow: visible;"><span style="font-family: &amp;quot;"><strong><span><span style="color: #859900;">var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">identity</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">WindowsIdentity</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">GetCurrent</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">();
</span><span><span style="color: #859900;">if</span></span><span style="color: #586e75;"> (</span><span><span style="color: #657b83;">identity</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">==</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">null</span></span><span style="color: #586e75;">) </span><span><span style="color: #859900;">throw</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">new</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">InvalidOperationException</span></span><span style="color: #586e75;">(</span><span><span style="color: #2aa198;">"Couldn't get the current user identity"</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);
</span><span><span style="color: #859900;">var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">principal</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">new</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">WindowsPrincipal</span></span><span style="color: #586e75;">(</span><span><span style="color: #657b83;">identity</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);

</span><span><span style="color: #93a1a1;">// Check if this user has the Administrator role. If they do, return immediately.</span></span>
<span><span style="color: #93a1a1;">// If UAC is on, and the process is not elevated, then this will actually return false.</span></span>
<span><span style="color: #859900;">if</span></span><span style="color: #586e75;"> (</span><span><span style="color: #657b83;">principal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">IsInRole</span></span><span style="color: #586e75;">(</span><span><span style="color: #00008b;">WindowsBuiltInRole</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Administrator</span></span><span style="color: #586e75;">)) </span><span><span style="color: #859900;">return</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">true</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;

</span><span><span style="color: #93a1a1;">// If we're not running in Vista onwards, we don't have to worry about checking for UAC.</span></span>
<span><span style="color: #859900;">if</span></span><span style="color: #586e75;"> (</span><span><span style="color: #00008b;">Environment</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">OSVersion</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Platform</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">!=</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">PlatformID</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Win32NT</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">||</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">Environment</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">OSVersion</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Version</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Major</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">&lt;</span></span><span style="color: #586e75;"> </span><span><span style="color: #2aa198;">6</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">)
{
     <span><span style="color: #93a1a1;">// Operating system does not support UAC; skipping elevation check.
</span></span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">     </span><span><span style="color: #859900;">return</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">false</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;
}

</span><span><span style="color: #859900;">int</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">tokenInfLength</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">Marshal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">SizeOf</span></span><span style="color: #586e75;">(</span><span><span style="color: #859900;">typeof</span></span><span style="color: #586e75;">(</span><span><span style="color: #859900;">int</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">));
</span><span><span style="color: #00008b;">IntPtr</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">tokenInformation</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">Marshal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">AllocHGlobal</span></span><span style="color: #586e75;">(</span><span><span style="color: #657b83;">tokenInfLength</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);

</span><span><span style="color: #859900;">try</span></span>
</strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">{</span><span><span style="color: #859900;">
    var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">token</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">identity</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Token</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;
</span></strong></span><span style="font-family: &amp;quot;"><strong><span><span style="color: #859900;"><span style="color: #586e75;">    </span>var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">result</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #008b8b;">GetTokenInformation</span></span><span style="color: #586e75;">(</span><span><span style="color: #657b83;">token</span></span><span style="color: #586e75;">, </span><span><span style="color: #00008b;">TokenInformationClass</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">TokenElevationType</span></span><span style="color: #586e75;">, </span><span><span style="color: #657b83;">tokenInformation</span></span><span style="color: #586e75;">, </span><span><span style="color: #657b83;">tokenInfLength</span></span><span style="color: #586e75;">, </span><span><span style="color: #859900;">out</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">tokenInfLength</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);

    </span><span><span style="color: #859900;">if</span></span><span style="color: #586e75;"> (</span><span><span style="color: #d33682;">!</span></span><span><span style="color: #657b83;">result</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">)
    {
        </span><span><span style="color: #859900;">var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">exception</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">Marshal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">GetExceptionForHR</span></span><span style="color: #586e75;">( </span><span><span style="color: #00008b;">Marshal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">GetHRForLastWin32Error</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">() );
        </span><span><span style="color: #859900;">throw</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">new</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">InvalidOperationException</span></span><span style="color: #586e75;">(</span><span><span style="color: #2aa198;">"Couldn't get token information"</span></span><span style="color: #586e75;">, </span><span><span style="color: #657b83;">exception</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);
    }

    </span><span><span style="color: #859900;">var</span></span><span style="color: #586e75;"> </span><span><span style="color: #657b83;">elevationType</span></span><span style="color: #586e75;"> </span><span><span style="color: #d33682;">=</span></span><span style="color: #586e75;"> (</span><span><span style="color: #00008b;">TokenElevationType</span></span><span style="color: #586e75;">)</span><span><span style="color: #00008b;">Marshal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">ReadInt32</span></span><span style="color: #586e75;">(</span><span><span style="color: #657b83;">tokenInformation</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">);
</span></strong></span><span style="font-family: &amp;quot;"><strong><span><span style="color: #859900;"><span style="color: #586e75;">    </span>
    switch</span></span><span style="color: #586e75;"> (</span><span><span style="color: #657b83;">elevationType</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">)
    {
     </span><span><span style="color: #859900;">   case</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">TokenElevationType</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">TokenElevationTypeDefault</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">:
            </span><span><span style="color: #93a1a1;">// TokenElevationTypeDefault - User is not using a split token, so they cannot elevate.</span></span>
<span style="color: #586e75;">            </span><span><span style="color: #859900;">return</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">false</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;
        </span><span><span style="color: #859900;">case</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">TokenElevationType</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">TokenElevationTypeFull</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">:
            </span><span><span style="color: #93a1a1;">// TokenElevationTypeFull - User has a split token, and the process is running elevated. Assuming they're an administrator.</span></span>
<span style="color: #586e75;">            </span><span><span style="color: #859900;">return</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">true</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;
        </span><span><span style="color: #859900;">case</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">TokenElevationType</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">TokenElevationTypeLimited</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">:
            </span><span><span style="color: #93a1a1;">// TokenElevationTypeLimited - User has a split token, but the process is not running elevated. Assuming they're an administrator.</span></span>
<span style="color: #586e75;">            </span><span><span style="color: #859900;">return</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">true</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;
        </span><span><span style="color: #859900;">default</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">:
            </span><span><span style="color: #93a1a1;">// Unknown token elevation type.</span></span>
<span style="color: #586e75;">            </span><span><span style="color: #859900;">return</span></span><span style="color: #586e75;"> </span><span><span style="color: #859900;">false</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">;
     }
}
</span><span><span style="color: #859900;">finally</span></span>
</strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">{     
</span><span><span style="color: #859900;">    if</span></span><span style="color: #586e75;"> (</span><span><span style="color: #657b83;">tokenInformation</span></span><span style="color: #586e75;"> </span><span><span style="color: #008b8b;">!=</span></span><span style="color: #586e75;"> </span><span><span style="color: #00008b;">IntPtr</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #800080;">Zero</span></span></strong></span><span style="font-family: &amp;quot;"><strong><span style="color: #586e75;">) </span><span><span style="color: #00008b;">Marshal</span></span><span><span style="color: #d33682;">.</span></span><span><span style="color: #008b8b;">FreeHGlobal</span></span><span style="color: #586e75;">(</span><span><span style="color: #657b83;">tokenInformation</span></span></strong><span style="color: #586e75;"><strong>);
}</strong></span></span></pre>

### Visual Basic 6 (VB6)

For Visual Basic 6, there’s some additional code, as we need to get the token for the current process, and use more calls to also get the operating system version.

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Type</span></span></span><span><span style="font-size: 10pt;"> OSVERSIONINFO</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">dwOSVersionInfoSize </span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span><span> </span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">dwMajorVersion </span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span><span> </span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">dwMinorVersion </span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">dwBuildNumber </span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">dwPlatformId </span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">szCSDVersion </span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">As</span></span><span> </span><span><span style="color: #00007f;">String</span></span><span> * </span><span><span style="color: #007f7f;">128</span></span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">End</span></span></span><span style="font-size: 10pt;"><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Type</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt; color: #007f00;">' dwPlatformId values</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Public</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Const</span></span><span> VER_PLATFORM_WIN32s = </span></span><span><span style="font-size: 10pt; color: #007f7f;"></span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Public</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Const</span></span><span> VER_PLATFORM_WIN32_WINDOWS = </span></span><span><span style="font-size: 10pt; color: #007f7f;">1</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Public</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Const</span></span><span> VER_PLATFORM_WIN32_NT = </span></span><span><span style="font-size: 10pt; color: #007f7f;">2</span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span>
</p>

<p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span style="font-family: &amp;quot;"><span> </span></span>
  </p>
  
  <p>
    <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Public</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Declare</span></span><span> </span><span><span style="color: #00007f;">Function</span></span><span> GetVersionEx </span><span><span style="color: #00007f;">Lib</span></span><span> </span><span><span style="color: #7f007f;">"kernel32&#8243;</span></span><span> </span><span><span style="color: #00007f;">Alias</span></span><span> </span><span><span style="color: #7f007f;">"GetVersionExA"</span></span><span> (</span><span><span style="color: #00007f;">ByRef</span></span><span> lpVersionInformation </span><span><span style="color: #00007f;">As</span></span><span> OSVERSIONINFO) </span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt; color: #007f00;">' These functions are for getting the process token information, which IsUserAnAdministrator uses to</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt; color: #007f00;">' handle detecting an administrator that's running in a non-elevated process under UAC.</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Private</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Const</span></span><span> TOKEN_READ </span><span><span style="color: #00007f;">As</span></span><span> </span><span><span style="color: #00007f;">Long</span></span><span> = </span></span><span><span style="font-size: 10pt; color: #007f7f;">&H20008</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Private</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Const</span></span><span> TOKEN_ELEVATION_TYPE </span><span><span style="color: #00007f;">As</span></span><span> </span><span><span style="color: #00007f;">Long</span></span><span> = </span></span><span><span style="font-size: 10pt; color: #007f7f;">18</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span style="font-family: &amp;quot;"><span style="line-height: 12pt;"><span style="color: #00007f;"><span style="font-size: 10pt;">Private</span></span></span><span style="font-size: 10pt;"><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Declare</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Function</span></span><span style="line-height: 12pt;"> IsUserAnAdmin </span><span style="line-height: 12pt;"><span style="color: #00007f;">Lib</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #7f007f;">"Shell32&#8243;</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Alias</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #7f007f;">"#680&#8243;</span></span><span style="line-height: 12pt;"> () </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> </span></span><span style="line-height: 12pt;"><span style="font-size: 10pt; color: #00007f;">Integer</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Private</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Declare</span></span><span> </span><span><span style="color: #00007f;">Function</span></span><span> CloseHandle </span><span><span style="color: #00007f;">Lib</span></span><span> </span><span><span style="color: #7f007f;">"kernel32&#8243;</span></span><span> (</span><span><span style="color: #00007f;">ByVal</span></span><span> hObject </span><span><span style="color: #00007f;">As</span></span><span> </span><span><span style="color: #00007f;">Long</span></span><span>) </span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
    <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Private</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Declare</span></span><span> </span><span><span style="color: #00007f;">Function</span></span><span> OpenProcessToken </span><span><span style="color: #00007f;">Lib</span></span><span> </span><span><span style="color: #7f007f;">"advapi32.dll"</span></span><span> (</span><span><span style="color: #00007f;">ByVal</span></span><span> ProcessHandle </span><span><span style="color: #00007f;">As</span></span><span> </span><span><span style="color: #00007f;">Long</span></span><span>, </span><span><span style="color: #00007f;">ByVal</span></span><span> DesiredAccess </span><span><span style="color: #00007f;">As</span></span><span> </span><span><span style="color: #00007f;">Long</span></span><span>, TokenHandle </span><span><span style="color: #00007f;">As</span></span><span> </span><span><span style="color: #00007f;">Long</span></span><span>) </span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
  </p>
  
  <p class="MsoNormal" style="line-height: 13pt; margin: 0cm 0cm 10pt;">
    <span style="font-family: &amp;quot;"><span style="line-height: 12pt;"><span style="color: #00007f;"><span style="font-size: 10pt;">Private</span></span></span><span style="font-size: 10pt;"><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Declare</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Function</span></span><span style="line-height: 12pt;"> GetTokenInformation </span><span style="line-height: 12pt;"><span style="color: #00007f;">Lib</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #7f007f;">"advapi32.dll"</span></span><span style="line-height: 12pt;"> (</span><span style="line-height: 12pt;"><span style="color: #00007f;">ByVal</span></span><span style="line-height: 12pt;"> TokenHandle </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Long</span></span><span style="line-height: 12pt;">, </span><span style="line-height: 12pt;"><span style="color: #00007f;">ByVal</span></span><span style="line-height: 12pt;"> TokenInformationClass </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Long</span></span><span style="line-height: 12pt;">, TokenInformation </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> Any,_<span style="font-family: &amp;quot;"><span style="font-size: 10pt;"><span style="line-height: 12pt;"><span style="color: #00007f;"> ByVal</span></span><span style="line-height: 12pt;"> TokenInformationLength </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Long</span></span><span style="line-height: 12pt;">, ReturnLength </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> </span><span style="line-height: 12pt;"><span style="color: #00007f;">Long</span></span><span style="line-height: 12pt;">) </span><span style="line-height: 12pt;"><span style="color: #00007f;">As</span></span><span style="line-height: 12pt;"> </span></span><span style="line-height: 12pt;"><span style="font-size: 10pt; color: #00007f;">Long</span></span></span></p> 
    
    <p>
      </span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="color: #00007f;"><span style="font-size: 10pt;">Public</span></span></span><span style="font-size: 10pt;"><span> </span><span><span style="color: #00007f;">Function</span></span><span> IsUserAnAdministrator() </span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Boolean</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">On</span></span><span> </span><span><span style="color: #00007f;">Error</span></span><span> </span><span><span style="color: #00007f;">GoTo</span></span></span><span><span style="font-size: 10pt;"> IsUserAnAdministratorError</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">IsUserAnAdministrator = </span></span><span><span style="font-size: 10pt; color: #00007f;">False</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">If</span></span><span> IsUserAnAdmin() </span></span><span><span style="font-size: 10pt; color: #00007f;">Then</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">IsUserAnAdministrator = </span></span><span><span style="font-size: 10pt; color: #00007f;">True</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Exit</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Function</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">End</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">If</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span><span style="font-size: 10pt; color: #007f00;">' If we're on Vista onwards, check for UAC elevation token</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span><span style="font-size: 10pt; color: #007f00;">' as we may be an admin but we're not elevated yet, so the</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span><span style="font-size: 10pt; color: #007f00;">' IsUserAnAdmin() function will return false</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Dim</span></span><span> osVersion </span><span><span style="color: #00007f;">As</span></span></span><span><span style="font-size: 10pt;"> OSVERSIONINFO</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">osVersion.dwOSVersionInfoSize = </span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Len</span></span></span><span><span style="font-size: 10pt;">(osVersion)</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">If</span></span><span> GetVersionEx(osVersion) = </span><span><span style="color: #007f7f;"></span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Then</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Exit</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Function</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">End</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">If</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">If</span></span><span> osVersion.dwPlatformId <> VER_PLATFORM_WIN32_NT </span><span><span style="color: #00007f;">Or</span></span><span> osVersion.dwMajorVersion < </span><span><span style="color: #007f7f;">6</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Then</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span><span style="font-size: 10pt; color: #007f00;">' If the user is not on Vista or greater, then there's no UAC, so don't bother checking.</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Exit</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Function</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">End</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">If</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Dim</span></span><span> result </span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Dim</span></span><span> hProcessID<span style="mso-spacerun: yes;"> </span></span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Dim</span></span><span> hToken<span style="mso-spacerun: yes;"> </span></span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Dim</span></span><span> lReturnLength<span style="mso-spacerun: yes;"> </span></span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Dim</span></span><span> tokenElevationType </span><span><span style="color: #00007f;">As</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Long</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span><span style="font-size: 10pt; color: #007f00;">' We need to get the token for the current process</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="font-family: &amp;quot;"><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">hProcessID = GetCurrentProcess()</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">If</span></span><span> hProcessID <> </span><span><span style="color: #007f7f;"></span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Then</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">If</span></span><span> OpenProcessToken(hProcessID, TOKEN_READ, hToken) = </span><span><span style="color: #007f7f;">1</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Then</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">result = GetTokenInformation(hToken, TOKEN_ELEVATION_TYPE, tokenElevationType, </span></span><span style="font-size: 10pt;"><span><span style="color: #007f7f;">4</span></span></span><span><span style="font-size: 10pt;">, lReturnLength)</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">If</span></span><span> result = </span><span><span style="color: #007f7f;"></span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Then</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span><span style="font-size: 10pt; color: #007f00;">' Couldn't get token information</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Exit</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Function</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">End</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">If</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span><span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">If</span></span><span> tokenElevationType <> </span><span><span style="color: #007f7f;">1</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Then</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">IsUserAnAdministrator = </span></span><span><span style="font-size: 10pt; color: #00007f;">True</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">End</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">If</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="font-family: &amp;quot;"><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="font-family: &amp;quot;"><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">CloseHandle hToken</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">End</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">If</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="font-family: &amp;quot;"><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span><span style="font-size: 10pt;">CloseHandle hProcessID</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">End</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">If</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"><span style="font-size: 10pt;"> </span></span></span><span style="font-size: 10pt;"><span><span style="color: #00007f;">Exit</span></span><span> </span></span><span><span style="font-size: 10pt; color: #00007f;">Function</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="mso-spacerun: yes;"><span style="font-family: &amp;quot;"><span style="font-size: 10pt;"> </span></span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span><span style="font-family: &amp;quot;"><span style="font-size: 10pt;">IsUserAnAdministratorError:</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: normal; margin: 0cm 0cm 0pt; mso-layout-grid-align: none;">
      <span style="font-family: &amp;quot;"><span><span style="mso-spacerun: yes;"> </span></span><span><span style="font-size: 10pt; color: #007f00;"> ' Handle errors</span></span></span>
    </p>
    
    <p class="MsoNormal" style="line-height: 13pt; margin: 0cm 0cm 10pt;">
      <span style="font-family: &amp;quot;"><span style="line-height: 12pt;"><span style="color: #00007f;"><span style="font-size: 10pt;">End</span></span></span><span style="font-size: 10pt;"><span style="line-height: 12pt;"> </span></span><span style="line-height: 12pt;"><span style="font-size: 10pt; color: #00007f;">Function</span></span></span>
    </p>
    
    <h2>
      References
    </h2>
    
    <p>
      <a href="http://blogs.msdn.com/b/cjacks/archive/2006/10/09/how-to-determine-if-a-user-is-a-member-of-the-administrators-group-with-uac-enabled-on-windows-vista.aspx">Blog Post by Chris Jackson: How to Determine if a User is a Member of the Administrators Group with UAC Enabled on Windows Vista</a>
    </p>