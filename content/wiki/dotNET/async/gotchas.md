---
title: Gotchas
description: "Do's and don'ts when working with async"
toc: true
---

# Async / Await Gotchas

Spot the bug:

```csharp
    internal Task<DataFormat> TestAsync()
    {
        using (var stream = File.Open("test.dat", FileMode.Open, FileAccess.Read, FileShare.Read))
        {
            return StreamProcessingUtil.DoSomethingAsync(stream);
        }
    }
```

Oops! We actually need to await the method that gets passed the stream, as without an await, the closing of the using will be hit, disposing the stream before our method has a chance to start or finish what it wants to do.

Solution:

```csharp
    internal async Task<DataFormat> TestAsync()
    {
        using (var stream = File.Open("test.dat", FileMode.Open, FileAccess.Read, FileShare.Read))
        {
            return await StreamProcessingUtil.DoSomethingAsync(stream);
        }
    }
```