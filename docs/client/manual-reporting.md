Manual reporting
================

Most of our client libraries detect and report unhandled exceptions. But sometimes you have your own `try`/`catch` blocks. In those you need to manually report errors.

This guide aims to explain how.

The most basic way is simply to invke `Err.Report()`:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    Err.Report(ex);
}
```

You can also attach context information:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    Err.Report(ex, yourContextData);
}
```


### Using anonymous object

If you need to attach multiple values you can use an anonymous object:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    Err.Report(ex, new { UserId = userId, UserState = state });
}
```

**Result**

![](anonymous-object.png)

Complex structures are supported.


# Creating custom context collections

You can also create custom context collections which will be automatically included with every error report.

[Read more](extending/contextprovider/)
