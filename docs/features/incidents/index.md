Error
=====

An error in Coderr is a distinct entity generated from one or more error reports in your application. A single error can be reported millions of times (and is for a few of our customers).

The error can either be an exception or a violation of your non-functional requirements. Errors can either be reported by you, your favorite logging library, or by one of our integration libraries.

## How Coderr determines what is a new error or not.

Coderr uses different methods to determine what's a unique error.

The most basic approach is to use the stack trace and the error type to group reports together. The method does differ depending on the error type and the client library that reported the error.

## Customizing incidents

You can override Coderr's default method of grouping error reports together. In that way, all errors with the same _hash source_ are grouped into a single error. You can use the same hash source from multiple places in your code, and the error reports still appear under the same error.

### Using a context provider

To do that, you can either include a property called `HashSource` in the `CoderrData` collection in a context data provider:

```csharp
public class ProcessorProvider : IContextInfoProvider
{
    // No need to provide a name since we do not add a new collection to the error report.
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

