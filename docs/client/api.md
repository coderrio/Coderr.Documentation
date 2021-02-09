API Specification
=================

The Coderr Reporting API is used to send error reports to Coderr for analysis. You can do this by yourself, or use one of the pre-existing clients to report errors.

The reporting API is based on HTTP where the error reports are gzipped and then signed with a HMAC hash code (using the shared secret).

# Uploading reports

The process works as following:

## 1. The Error report is serialized to JSON.

The error report DTO (json schema, minimal example) is serialized to JSON, then it's converted to a byte stream using the UTF8 encoding.

In .NET it looks like:

```csharp
var reportJson = JsonConvert.SerializeObject(reportDTO, Formatting.None,
    new JsonSerializerSettings
    {
        TypeNameHandling = TypeNameHandling.None,
        ContractResolver =
            new IncludeNonPublicMembersContractResolver()
    });
var jsonBytes = Encoding.UTF8.GetBytes(reportJson);
```

The report itself is identified by the `ErrorId` property which also can be used to attach user feedback / bug reports to the error report at a later stage.

## 2. GZipped

To reduce the amount of data required to upload the report, it's gzipped. The gzip step is optional, some HTTP clients supports GZIP out of the box and it can therefore make sense to let the HTTP client do that.

```csharp
var ms = new MemoryStream();
using (var gzip = new GZipStream(ms, CompressionLevel.Optimal, true))
{
    gzip.Write(jsonBytes, 0, jsonBytes.Length);
    gzip.Flush();
}
var requestBody = ms.ToArray();
```

## 3. Sign the report

Once the report has been serialized and (optionally) compressed, it's time to sign the report to be able to tell that it came from a trusted client.

That is done by using HMAC/SHA256 and the Shared Secret which is provided by Coderr.

```csharp
var sharedSecret = "5aeb7154336d48168f41042b11a6dd7b";
var hashAlgo = new HMACSHA256(Encoding.UTF8.GetBytes(sharedSecret));
var hash = hashAlgo.ComputeHash(requestBody, 0, requestBody.Length);
var signature = Convert.ToBase64String(hash);
```

Once that is done, the report is ready to upload.

## 4. Upload the report

Reports should be uploaded to "`https://yourserver/coderr/receiver/report/{apiKey}/?sig={signature}`", where "`{apiKey}`" should be replaced with the API-key defined in the Coderr UI, and "`{signature}`" is replaced with the generated hash. 
For Coderr Cloud the URI should be "`https://report.coderr.io/receiver/report/{apiKey}/?sig={signature}`".

# Example report

This is a minimal error report:

```javascript
{
	"CreatedAtUtc": "2021-02-01T10:00:00",
	"ContextCollections": [
		{
			"Name": "CoderrData",
			"Properties": {
				"Hello": "Test",
				"AppAssemblyVersion": "1.0.0.0",
				"ErrPartition.UserId": "17"
			}
		},
	],
	"Exception": {
		"StackTrace": "  at a1d6f895e23645b283b3e8af73242a8f:line 40\r\n   at TestReporter.Console.Tools.Reporter.CreateException(String message) in D:\\src\\1tcompany\\coderr\\Commercial\\Server\\src\\Tools\\TestReporter\\ConsoleApp1\\TestReporter.Abstractions\\Tools\\Reporter.cs:line 56",
		"Message": "Something failed.",
		"Name": "InvalidOperationException",
		"Namespace": "System",
	},
	"ReportId": "OBEDpAB5jUe71Enlay42KA",
	"ReportVersion": "1.0",
	"EnvironmentName": "IntegrationTests",
	"LogEntries": [{
		"Level": 1,
		"Message": "This is a log entry",
		"Source": "MyClass",
		"TimeStampUtc": "2021-02-01T10:00:00"
	}]
}
```

# Controlling Coderr

You can control different features in Coderr by specifying different keys in a special context collection named "`CoderrData`".

The following configuration options are simply key/values in that collection.

## Tags

You can categorize errors by using [tags](/features/incidents/tags). To include tags, add a key to the collection named "`ErrTags`". It's value should be a comma-separated list, for instance "`important,backend`".

### Example

```javascript
{
    // [.. the rest of the JSON document ..]
    "ContextCollections": {
        {
            "Name": "CoderrData",
            "Properties": {
                "ErrTags": "important,backend",
            }
        }
    }
}
```

## Position

Sometimes, errors only occur in a specific geographic region. Coderr tracks locations by converting the IP address to a location, but you can also override that behavior by including "`Longitude`" and "`Latitude`" in the collection.

### Example

```javascript
{
    // [.. the rest of the JSON document ..]
    "ContextCollections": {
        {
            "Name": "CoderrData",
            "Properties": {
                "Latitude": "38.889248",
                "Longitude": "-77.050636"
            }
        }
    }
}
```

## Application version

All errors are not reported in every application version, and you might have several versions deployed.
It therefore makes sense to track which application versions that an error exists in.

### Example

```javascript
{
    // [.. the rest of the JSON document ..]
    "ContextCollections": {
        {
            "Name": "CoderrData",
            "Properties": {
                "AppAssemblyVersion": "1.5.2",
            }
        }
    }
}
```

## Prioritizing errors

Coderr can prioritize errors based on the actual affect on your business.
That's done by providing metrics. For instance, if number of affected users is the most important metric, attach the user id.

For partitions, they should be prefixed with "`ErrPartition.`".

Try to keep the values as short as possible in high load systems.

### Example

```javascript
{
    // [.. the rest of the JSON document ..]
    "ContextCollections": {
        {
            "Name": "CoderrData",
            "Properties": {
                "ErrPartition.ServerName": "EU-NE-SRV2421",
            }
        }
    }
}
```

## Controlling errors

You can override Coderr's algorithm which identifies unique errors by providing your own identifier.

That's done by providing the "`HashSource`" key in the collection. To Coderr, the string is considered opaque, but must be the same for all error reports that are for the same error.

```javascript
{
    // [.. the rest of the JSON document ..]
    "ContextCollections": {
        {
            "Name": "CoderrData",
            "Properties": {
                "HashSource": "Backend.Connection.Lost",
            }
        }
    }
}
```

## Grouping related errors

Coderr have a related errors feature that can be used to navigate a set of errors that are related.

That's done with the help of the "`CorrelationId`" key. It must be the same for all errors that are related.

```javascript
{
    // [.. the rest of the JSON document ..]
    "ContextCollections": {
        {
            "Name": "CoderrData",
            "Properties": {
                "CorrelationId": "lkds48djd",
            }
        }
    }
}
```

## Quick facts

When you look at an error in the Coderr UI, there is a quick-fact pane to the right.

You can attach information that should be visible in that box. Do note that all values will be added to the key. If you report 500 errors which all have different values, the quick fact box will be filled with all 500 values.

Quick-facts should be prefixed with "`QuickFact.`".

```javascript
{
    // [.. the rest of the JSON document ..]
    "ContextCollections": {
        {
            "Name": "CoderrData",
            "Properties": {
                "QuickFact.ProtocolVersion": "2.1",
            }
        }
    }
}
```
