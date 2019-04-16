---
title: "MSBuild"
description: "MSBuild"
toc: true
menu:
    wiki:
        parent: net
---
# Carriage return line feed

You can escape the carriage return line feed using `%0A` and `%0D` respectively.

# Display item lists

This will print out the items on their own line:

```xml
<Message Text="Items: @(Items, '%0a%0d')" />
```
