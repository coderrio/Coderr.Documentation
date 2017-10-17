log4net configuration
=====================

If you have not done that yet, install the nuget package called `coderr.client.log4net`.

Next, you need to tell the codeRR library what it should upload all error reports to.

Add the following code in your `Program.cs` (or the starting point of the framework that you use).

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
Err.Configuration.CatchLog4NetExceptions();
```

It must be added after the log4net configuration, but before the first usage of `LogManager.GetLogger()`.

Try to log an exception to see if it works.

```csharp
try
{
    throw new Exception("Oooop");
}
catch (Exception ex)
{
    _logger.Error("Testing codeRR", ex);
}
```

The error should appear in the codeRR server shortly after being reported.

## More information

Read how you can [report errors manually](../../gettingstarted.md)