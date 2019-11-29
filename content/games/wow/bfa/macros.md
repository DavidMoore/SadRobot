---
title: Paladin Macros
description: Macros and recommended interface mods for Paladins
menu:
    games:
        parent: "bfa"
        weight: 50
---

#### Avenger's Shield

Casts at mouseover enemy, focus target enemy or current target
If you're in PvP and holding CTRL, then enable Shield of Virtue (AOE silence) before throwing shield

```
  #showtooltip Avenger's Shield
  /cast [mod:ctrl] Shield of Virtue
  /cast [@mouseover,harm,nodead][@focus,harm,nodead][@target,harm,nodead]Avenger's Shield
```

#### Rebuke

Kick / interrupt your mouseover target, focus target or selected target (in that priority order)

```
  #showtooltip
  /stopcasting
  /cast [@mouseover,harm,nodead][@focus,harm,nodead][@target,harm,nodead] Rebuke
```

#### Hammer of Justice

```
#showtooltip
/cast [@mouseover,exists,harm][] Hammer of Justice
```

#### Judgment

Judges your mouseover target if they're an enemy, enemy focus target or finally your target.

```
  #showtooltip
  /cast [@mouseover,exists,harm][@focus,exists,harm][@target,harm,nodead][]Judgment
```

#### Divine Shield

Casts Divine Shield, and hit it again to cancel your immunity. Use this when doing bubble taunt combos or using bubbles to reset stacks or cheese mechanics.

```
#showtooltip Divine Shield
/stopcasting
/cancelaura Divine Shield
/cancelaura Blessing of Protection
/cast Divine Shield
```

#### Light/Hand of the Protector

Cast Light of the Protector / Hand of the Protector on your mouseover target, selected target or yourself.

```
#showtooltip
/cast [@mouseover,exists][@target,exists][@player]Light of the Protector
```