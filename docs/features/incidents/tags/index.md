Tags
====

Tags allow you to categorize errors.

To attach tags to an incident you can do the following:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    Err.Report(ex, new { ErrTags = "important,backend" });

    // alternative:
    // Err.Report(ex, new { ErrTags = new[] { "important", "backend" }});
}
```

### Result

![](/screens/features/tags/tags-ui.png)


## Add a tag to every report

To add an tag to every report (like a server name), you can use a [custom context provider](../../../client/extending/contextprovider/).

```csharp
public class ServerNameProvider : IContextInfoProvider
{
    public string Name => "ServerName";

    public ContextCollectionDTO Collect(IErrorReporterContext context)
    {
        var properties = new Dictionary<string, string>();
        properties.Add("ErrTags", Environment.MachineName);

        return new ContextCollectionDTO(Name, properties);
    }
}
```

The .NET Standard version of the interface is named `IContextCollectionProvider` instead of `IContextInfoProvider`.

To activate the provider, register it using `Err.Configuration`:

```csharp
Err.Configuration.ContextProviders.Add(new ServerNameProvider());
```

### Result

![](/screens/features/tags/context-collection.png)


## Finding incidents using tags

Once you have added tags you can use them to find specific incidents in the search interface:

![](/screens/features/tags/incident-search.png)

