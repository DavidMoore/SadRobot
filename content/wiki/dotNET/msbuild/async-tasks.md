# Async Tasks

You can use async / await:

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
