Core configuration instructions
===========================

Install the nuget package called `coderr.client`.

Next, you need to tell the Coderr library what server it should upload all error reports to.

Add the following code in your `Program.cs` (or the starting point of the framework that you use).

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

The appKey and the sharedSecret can be found in the Coderr server.

Once configured, start your application and try manually to report an exception.

You can add the following code somewhere and then invoke your application:

```csharp
try
{
    throw new Exception("Hello world");
}
catch (Exception ex)
{
    Err.Report(ex, new { SampleData = "Context example"});
}
```

## More information

If you want more information, read the  [client documentation](index.md) or on error reporting [report errors](/getting-started)
