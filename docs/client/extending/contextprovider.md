Creating a custom context provider
==================================

Context providers are used to automatically attach information to each error report. The information is useful to determine why an exception have been thrown.

![](/screens/features/context/anonymous-object.png)

To create a provider you need to create a class which implements the context provider interface. In the .NET standard library the interface is named `IContextCollectionProvider`.

Then register the provider using `Err.Configuration.ContextProviders.Add(new YourProvider());`.

## .NET Standard example

Here is a sample for .NET Core MVC:

```csharp
public class SampleProvider : IContextCollectionProvider
{
    /// <inheritdoc />
    public ContextCollectionDTO Collect(IErrorReporterContext context)
    {
        if (!(context is MvcCoreErrorContext aspNetContext) || aspNetContext.ViewBag == null)
            return null;

        var properties = new Dictionary<string,string>();
        properties["CurrentUser"] = Thread.CurrentPrincipal.Identity.Name;
        properties["ErrTags"] = "fatal";

        return new ContextInfoCollection(Name, properties);
    }

    /// <inheritdoc />
    public string Name => "MyData";
}
```

There is also a helper class which can convert .NET objects into context collections:

```csharp
public class ViewBagProvider : IContextCollectionProvider
{
    /// <inheritdoc />
    public ContextCollectionDTO Collect(IErrorReporterContext context)
    {
        if (!(context is MvcCoreErrorContext aspNetContext) || aspNetContext.ViewBag == null)
            return null;

        var converter = new ObjectToContextCollectionConverter();
        return converter.Convert(Name, aspNetContext.ViewBag);
    }

    /// <inheritdoc />
    public string Name => "ViewBag";
}
```

## Getting information from the .NET library

In most cases you need to be able to get information from your favorite .NET framework/library. For that Coderr provides a context that you can use to extract information.

The context is different for each Coderr client library. Here is a list of all available contexts.

Client name | URL
----------- | ---------
Base library | `if (context is ErrorReporterContext errorContext) ....`
ASPNET | `if (context is HttpErrorReporterContext httpContext) ....`
ASPNET MVC5 | `if (context is AspNetMvcContext aspNetContext) ....`
ASPNET Core | `if (context is MvcCoreErrorContext mvcContext) ....`
WPF | `if (context is WpfErrorReporter wpfContext) ....`
WinForms | `if (context is WinformsErrorReportContext winFormsContext) ....`

The `if` is required if you are using multiple libraries in your application, since errors will then run through different Coderr pipelines.

# Conventions

A couple of conventions which can be used within your collector.

## Exceptions during collection

A context info provider MUST not throw exceptions. Therefore you need to have a catch all which wraps your logic. You can however include the exception within your context collection to be able to analyze the exception in our UI.

```csharp
var properties = new Dictionary<string,string>();
try
{
    properties["CurrentUser"] = Thread.CurrentPrincipal.Identity.Name;
}
catch (Exception ex)
{
    properties["CurrentUser.Error"] = ex.ToString();
}
return new ContextInfoCollection("YourCollectionName", properties);
```

## Adding tags

You can add tags to error reports by using a context collection property named `ErrTags`:

```csharp
var properties = new Dictionary<string,string>();
try
{
    properties["CurrentUser"] = Thread.CurrentPrincipal.Identity.Name;
    properties["ErrTags"] = "fatal";
}
catch (Exception ex)
{
    properties["CurrentUser.Error"] = ex.ToString();
}

return new ContextInfoCollection("YourCollectionName", properties);
```


