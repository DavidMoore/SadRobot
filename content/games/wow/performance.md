---
title: "Settings & Performance"
description: System settings for graphics performance
toc: true
menu:
    games:
        parent: "wow"
        weight: 40
        name: "Settings"
---

# UI Scale

Set the UI scale to 768 / (screen height.

e.g. 768 / 1440 = 0.5333

/script print(GetCVar("useUiScale"))
/script print(GetCVar("uiScale"))
/script print(UIParent:GetScale())

/script SetCVar("useUiScale", 1);
/script SetCVar("uiScale", 0.53333);
/script UIParent:SetScale(0.5333)

# System > Graphics

Always have these on:

Project Textures (``SET projectedTextures "1.000000"``)

Projected textures are usually used for ground visual effects for important mechanics in dungeons and raids; if you don't have them enabled, you will often not be able to see these mechanics and die to them.


Anti-Aliasing:



# System > Advanced

| Setting | Description | Recommendation |
|----------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| Triple Buffering | Smooths out framerate and eliminates tearing, but introduces input lag. | Disabled  |
| Reduce Input Lag | Reduces input lag but can impact framerate | Disabled |
| MSAA | Configures the colour / depth of MSAA setting | None |
| Multisample Alpha-test | Sample frequency rather than pixel frequency for MSAA | Enabled |
| Post-process AA |   |  CMAA  |
| Resample Quality |    |  None / Bilinear / Bicubic   |
| Graphics API | DirectX 11 / DirectX 12 | Set to the highest available |
| Physics Interactions | Physics interactions with environment | None / Player Only / Player and NPC |
| Graphics Card |    | Auto Detect |
| Max Foreground FPS |   |     |
| Max Background FPS |   |     |
| Contrast  |    |     |
| Brightness   |    |    |
| Gamma    |    |     |

Triple Buffering: Disabled, so you don't get input lag
Reduce Input Lag: Disabled

Max Foreground FPS:

If using G-Sync or V-Sync, set to a frame or two above the maximum refresh rate of your monitor, and disable V-Sync.

# Multi-Threading settings

```
SET gxMTPrepass "1"
SET gxMTOpaque "1"
SET gxMTDisable "0"
SET gxMTBeginDraw "1"
SET gxMTShadow "1"
```

## References

