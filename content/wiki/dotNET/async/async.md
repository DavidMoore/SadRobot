---
title: Overview
description: An overview of asynchronous programming approaches in .NET
toc: true
weight: 10
menu:
    wiki:
        name: "Overview"
        parent: "net"
        weight: 10
---

# Asynchronous Programming Model (APM): C# 1.0 /  .NET 1.0 Style

Legacy model using the `IAsyncResult` pattern.

Asynchronous calls are made using Begin and End methods on an API, with callbacks and state being passed between them.

```CSharp
public class MyClass  
{  
    public IAsyncResult BeginRead( byte [] buffer, int offset, int count, AsyncCallback callback, object state);
    public int EndRead(IAsyncResult asyncResult);  
}
```

## Exception handling

Exceptions can be thrown from BeginRead (such as trying to read from a stream that has already been closed). Unexpected errors occurring during the async request (e.g. I/O error when reading a file), occur on the thread pool thread and will throw an exception when calling EndRead.

# Event-based Asynchronous Pattern (EAP): C#2.0 / .NET 2.0 Style

```CSharp
public class MyClass  
{  
    public void ReadAsync(byte [] buffer, int offset, int count);  
    public event ReadCompletedEventHandler ReadCompleted;  
}
```

# Task-based Asynchronous Pattern (TAP): .NET 4.0 onwards

The modern recommended asynchronous programming model, wrapping asynchronous operations in a single approach, and adding first-class async keywords ``async`` and ``await`` to the language.

```
public class MyClass  
{  
    public Task<int> ReadAsync(byte [] buffer, int offset, int count);  
}
```


# References

[Asynchronous programming patterns @ MSDN](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/index)