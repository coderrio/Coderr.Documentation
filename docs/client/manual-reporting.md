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

### Custom context collections

We also have an object overload which can transform any object into a context collection (one of the groups in the "Context Data" menu in the codeRR website).

Below we are using `ToContextCollection()` extension method which can transform any object (including complex objects) into a context collection.


```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    var modelCollection = viewModel.ToContextCollection("ViewModel");
    var loggedInUser = User.ToContextCollection("User");
    Err.Report(ex, new[]{modelCollection, loggedInUser});
}
```

**Result**

![](attach_multiple_collections.png)

Hence you can easily attach and group your information just as you like.