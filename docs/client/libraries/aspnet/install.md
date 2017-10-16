ASP.NET configuration
=====================

To start with, you need to tell the codeRR library where it should upload all error reports.

You typically add this code in your `global.asax` (copy/paste).

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
```

If you want codeRR to automatically report all unhandled exceptions you need to add this line too:

```csharp
Err.Configuration.CatchAspNetExceptions();
```


## More information

[Client documentation](index.md) | [Reporting errors](../../gettingstarted.md)

