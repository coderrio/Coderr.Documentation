WPF client library
==================

The WPF client library handles unhandled exceptions, includes your view models and can help you display error pages and take screenshot of the active window.

## Expectations

This page expects that you have installed the WPF nuget packaged and configured it. If you have not, read the [configuration page](configure.md).


## Error pages

An error page can optionally be displayed.  When a new error is detected, Coderr will now display this:

![](/screens/libraries/winforms/winforms_error_minimal.png)

To activate and configure the feature, add the following line(s) below the other Coderr configuration lines in `app.xaml.cs`:

```csharp
// Add a leave feedback text area.
Err.Configuration.UserInteraction.AskUserForDetails = true;

// Ask user if an report may be uploaded.
Err.Configuration.UserInteraction.AskUserForPermission = true;

// Allow user to get notified once you have corrected the issue.
Err.Configuration.UserInteraction.AskForEmailAddress = true;
```

Examples:

![all flags set](/screens/libraries/winforms/winforms_error_all.png)

![only ask for permission](/screens/libraries/winforms/winforms_error_permission.png)

![only details](/screens/libraries/winforms/winforms_error_details.png)

![only email](/screens/libraries/winforms/winforms_error_email.png)

## WPF Error handling pipeline

By default, Coderr marks all exceptions as handled in WPF, which means that your application will not crash when an exception is detected.

If you want to prevent that, use the following setting.

```csharp
Err.Configuration.DoNotMarkExceptionsAsHandled();
```

## Context information

The context collections are included in the WPF library.

### OpenForms

Coderr collects information from all open forms using reflection. 

The information includes all controls and their configuration (position, content, visibility etc)

![Control content is included](/screens/libraries/wpf/winforms_open_forms.png)

### Screenshots

Screenshots can be activated by one of the following configuration lines:

```csharp
Err.Configuration.TakeScreenshots();
```

You will see the following under the incident in your Coderr server:

![](/screens/libraries/wpf/open_windows.png)

### View models

Coderr collects information from all viewModels in the open forms.

![](/screens/libraries/wpf/viewmodels.png)


# What to do next

* [Getting started guide](/getting-started/) - Guide to quickly get started with Coderr.
* [Coderr Cloud](https://coderr.io/try/cloud/) - Our cloud service.
* [Server installation](https://coderr.io/documentation/server/installation/) - How to install the Community Server (AGPL licensed)
