Customize report uploads
========================

The default configuration of the report uploader only attempts one time and then throws the report away.

You can change that behavior by telling the client library to queue reports:

```csharp
Err.Configuration.QueueReports = true;
```

Then the library will make three attempts per error report and can queue up to 10 reports in memory.

## Customizing behavior

To further customize behavior, you need to add the report uploader manually.

Remove the `Err.Configuration.Credentials()` line from your code and add the following instead:

```csharp
// Initialization
var uri = new Uri("https://report.coderr.io/");

var uploader = new UploadToCoderr(uri, "yourOwnAppKey", "yourOwnSharedSecret");

// Max number of reports that can be queued.
uploader.MaxQueueSize = 10;

//number of attempts per report
uploader.MaxAttempts = 1;

Err.Configuration.Uploaders.Register(uploader);
```

## Persistent queues

If you want to store error reports on disk until successful upload you need to create your own uploader class. 

Implement the  `IReportUploader` interface. You can use the `UploadToCoderr` class internally for the actual report. Use the `UploadToCoderr.UploadReportNow()` for the actual transfer.
