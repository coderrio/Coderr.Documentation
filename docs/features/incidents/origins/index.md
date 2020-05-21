Origins
=======

Origins allow you to see where the error reports come from.
With origins you can easily see if the incident is due to cultural differences or due to localization issues.

![](/screens/features/origins/falun.png)

## Customizing origins

Per default, Coderr use the IP address to lookup the origin of the report.
You can however customize which longitude and latitude to use.

```csharp
 try
{
    StoreDiscount();
}
catch (Exception ex)
{
    Err.Report(ex, new
    {
        ReportLatitude = "60.6065",
        ReportLongitude = "15.6355"
    });
}
```

## Using a context provider

If you are using context provider, you can add them to the Coderr collection:

```csharp
class LocationContextProvider : IContextInfoProvider // Named IContextCollectionProvider in the .NET standard library
{
    public ContextCollectionDTO Collect(IErrorReporterContext context)
    {
        // Only required for the .NET 4.6 library
        var v2Context = context as IErrorReporterContext2;

        var collection = v2Context.GetCoderrCollection();
        collection.Properties["Latitude"] = // pull here from wherever
        collection.Properties["Longitude"] = // pull here from wherever

        // return null to tell that we did not add a custom collection
        return null;
    }

    /// <summary>
    /// No name required since we do not add a collection
    /// </summary>
    public string Name { get; } = "NonName";
}
``` 

Finally register it to the Coderr pipeline:

```csharp
Err.Configuration.ContextProviders.Add(new LocationContextProvider());
```

