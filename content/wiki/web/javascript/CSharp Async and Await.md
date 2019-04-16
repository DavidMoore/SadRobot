---
title: CSharp Async & Await
---

# Asynchronous programming in C#

##  APM: C# 1.0 /  .NET 1.0 Style

This is known as the **Asynchronous Programming Model (APM)** and is associated with the `IAsyncResult` pattern.

Asynchronous calls are made using Begin and End methods on an API, with callbacks and state being passed between them.



```CSharp



```

### Exception handling

Exceptions can be thrown from BeginRead (such as trying to read from a stream that has already been closed). Unexpected errors occurring during the async request (e.g. I/O error when reading a file), occur on the thread pool thread and will throw an exception when calling EndRead.

## EPM: C#2.0 / .NET 2.0 Style


# References

[Asynchronous Programming Patterns @ MSDN](https://msdn.microsoft.com/en-us/library/jj152938.aspx)
