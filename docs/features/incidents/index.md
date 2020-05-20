Incidents
===========

An incident is an unique error, a group of error reports for the same error. The error can either be an exception or a violation of your non-functional requirements.

## How Coderr determines what is an new error or not.

Coderr uses different methods to determine what's an unique error.

The most basic approach is to use the stack trace and the error type to group reports together. The method do although differ depending on the error type and the client library that reported the error.

## Customizing incidents

You can override Coderr's default method of grouping errors together. In that way, all errors that have the same _hash source_ will be grouped together. It doesn't matter if they are reported in the same or in different classes.

### Using a context provider

Do do that you can either include a property called `HashSource` in the `CoderrData` collection in a context data provider:

```csharp
public class ProcessorProvider : IContextInfoProvider
{
    // No need to provide a name since we will not add a new collection to the error report.
    public string Name => "NoNameRequired";

    public ContextCollectionDTO Collect(IErrorReporterContext context)
    {
        var sqlContext = context as SqlContext;
        if (sqlContext == null)
            return null;

        // Create new incidents based on the SQL query.
        var collection = context.Collections.GetCoderrCollection();
        collection.Properties["HashSource"] = sqlContext.SqlCommand.CommandText;
    }
```


### When manually reporting an error

You can also add a `ErrorHashSource` property when reporting an exception:

```csharp
try
{
    SomeBusinessLogic();
}
catch (Exception ex)
{
    Err.Report(ex, new { ErrorHashSource: "SaveUser" });
}
```

### Using a report filter

Here is an example that takes the reports for a specific url and cuts away a GUID from the url.

```csharp
internal class BundleUploadRequests : IReportFilter
{
	public void Invoke(ReportFilterContext context)
	{
		var collection = FindUrl(context);
		if (collection == null)
			return;

		var property = collection.Properties.FirstOrDefault(x => x.Key == "Url");
		var pos = property.Value.LastIndexOf('/');
		if (pos != -1)
        {
            collection.Properties["ErrorHashSource"] = property.Value.Remove(pos);
        }
	}

	private static ContextCollectionDTO FindUrl(ReportFilterContext context)
	{
		string url;
		return (
			from collection in context.Report.ContextCollections
			from property in collection.Properties
			where property.Key == "Url" && property.Value.Contains("/upload/")
			select collection
		).FirstOrDefault();
	}
}
```

Register it by using:

```csharp
Err.Configuration.FilterCollection.Add(new BundleSlowReportPosts());
```

