---
title: Paladin Macros
description: Macros and recommended interface mods for Paladins
menu:
    games:
        parent: "wow"
        weight: 50
---

## Macros

### Avenger's Shield

Casts at mouseover enemy, focus target enemy or current target
If you're in PvP and holding ALT, then enable Shield of Virtue (AOE silence) before throwing shield

```
  #showtooltip Avenger's Shield
  /cast [mod:ctrl] Shield of Virtue
  /cast [@mouseover,harm,nodead][@focus,harm,nodead][@target,harm,nodead]Avenger's Shield
```

### Rebuke

```
  #showtooltip Rebuke
  /stopcasting
  /cast [@mouseover,harm,nodead][@focus,harm,nodead][@target,harm,nodead] Rebuke
```

### Judgment

```
  #showtooltip Judgment
  /cast [@mouseover,harm][@focus,exists,harm][] Judgment
```

### Divine Shield

```
#showtooltip Divine Shield
/stopcasting
/cancelaura [mod:ctrl] Divine Shield
/cancelaura [mod:ctrl] Blessing of Protection
/cast Divine Shield
```

### Light/Hand of the Protector

```
#showtooltip
/cast [@mouseover,exists][@target,exists][@player]Light of the Protector
```