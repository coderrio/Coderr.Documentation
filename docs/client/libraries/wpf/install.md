WPF configuration
=================

If you have not done that yet, install the nuget package called `coderr.client.wpf`.

Next, you need to tell the codeRR library where it should upload all error reports to.

Add the following code in your `App.xaml.cs`.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
Err.Configuration.CatchWpfExceptions();
```

Once done, all unhandled exceptions should be reported to codeRR.

Try to log an exception to see if it works.

```csharp
public void YourButton_Click()
{
    try
    {
        throw new Exception("Oooop");
    }
    catch (Exception ex)
    {
        _logger.Error("Testing codeRR", ex);
    }
}
```

The error should appear in the codeRR server shortly after being reported.

## More information

Did you know that codeRR can also take screenshots of your application forms when an error is detected? 

Or display error pages like the one below?

![](../winforms/winforms_error_all.png)

Want to dig deeper? Read the [client documentation](index.md) or how you can [report errors manually](../../gettingstarted.md)
