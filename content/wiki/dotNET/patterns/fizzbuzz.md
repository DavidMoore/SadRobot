---
title: "Fizz Buzz"
toc: true
description: "An implementation of the Fizz Buzz exercise in C#"
menu:
    wiki:
        name: "Fizz Buzz"
        parent: "net"
        weight: 100
---



```csharp
var numbers = Enumerable.Range(1, 100);

foreach(var value in numbers)
{
    var fizz = value % 3 == 0;
    var buzz = value % 5 == 0;
    
    if( !fizz && !buzz ) continue;
    
    if( fizz ) Console.Write("Fizz");    
    if( buzz ) Console.Write("Buzz");
    Console.WriteLine();
}
```
