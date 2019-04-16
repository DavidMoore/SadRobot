---
title: Async Tasks
description: Using async code in custom MSBuild tasks
---
# Async Tasks

You can use async in MSBuild tasks using a pattern like this:

```
public class MyCustomTask : Task {

    public override bool Execute()
    {
        return ExecuteAsync().GetAwaiter().GetResult();
    }

    protected async Task<bool> ExecuteAsync()
    {
         // Async / await code goes here
         
         // Return the result
         return true;
    }
}

```

Here, the default Task Execute implementation simply calls an async method (in a synchronous manner obviously).

This allows you to consume APIs that expose async methods, as the async/await becomes more pervasive.