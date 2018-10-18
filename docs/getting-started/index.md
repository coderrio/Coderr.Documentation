Getting started
===============

This document gives a technical overview of Coderr, installation help and how you configure and use Coderr.

# Installing the server

Coderr is a client/server solution which means that you either need to install a server somewhere or use our hosted solution.

Coderr Server is available as three different editions.

<table><tr><td valign="top" style="width:30%">

### Coderr Live

Our hosted service with a complete feature set. We make sure that everything is running and that the latest stable version is installed.

[Register an account](https://lobby.coderr.io)

</td><td valign="top" style="width:30%">

### Coderr Premise

Locally installed server with a complete feature set, Activate Directory support, team management and windows authentication.

[Download]()

</td><td valign="top" style="width:30%">

### Coderr Community Server

Open source server.

[Github page](https://github.com/coderrio/coderr.server)

</td></tr></table>

Choose one and make sure that you have either registered an account or installed it. You can also [compare the editions](https://coderr.io/features/compare/).

# Configuring your application

To let Coderr discover errors and collect information about them you need to install one of our nuget packages in your application. We support both .NET Standard and .NET 4.x.

We have two types of nuget packages. 

## Core libraries

Our core nuget libraries [Coderr.Client](https://coderr.io/documentation/client/libraries/core/) (.NET 4.x base library) and [Coderr.Client.NetStd](https://coderr.io/documentation/client/libraries/netstd/install.md) (.NET Standard 1.6 and above) are used to report and upload errors to the Coderr server. 

You can use them directly or install one of our automation libraries.

## Automation libraries

Coderr can detect and report all unhandled exceptions (and other types of errors). To activate that feature you need to install one of our automation libraries. Once done Coderr will detect exceptions and collect information related to the error like HTTP requests, screenshots, view models and more. The goal is to make it easy to understand why the exception was thrown.

When you start using Coderr, it's typically not crucial that you log relevant information using your logging library, as Coderr typically includes all information that you need to understand the error.

To get help to install and configure our nuget libraries, read the  article below.

[Using the client libraries](https://coderr.io/documentation/client/)
[Reporting errors](https://coderr.io/documentation/)

# Working with Coderr

A typical error handling flow consists of distinct steps that you need to take when working with errors.

![](steps.png)

1. You need to discover errors. Traditionally it's typically done by scanning log files or by receiving errors reports from users.
2. Once you receive an error report, you need to see if it's for an already known error or if for a new one.
3. When you have a list of errors, you want to work with the most important one. 
4. When you have selected an error, you need to be able to reproduce it so that you are sure that you are correcting the correct part of the code base.
5. Once you are sure about the cause, you can correct the error.

Coderr helps with all steps above except the last one. 

Coderr have been designed with that flow in mind to make it as easy as possible to identify, priortize and correct errors. There are three main sections.

![](topmenu.png)

* **Discover** - The starting point in Coderr. Used to find the incidents that should be corrected first. Once you found one, click "Assign to me" on it.
* **Analyze** - All incidents assigned to you will be found here, including all collected context data.
* **Deployment insights** - See how well your team has handled errors in each application release. Do the number of distinct errors increase or decrease?

All data can be filtered by using the application selection menu which can be seen to the far left. Click on it to see errors for one application only or for all applications.

## Finding errors to work with

Use the "Discover" menu to find errors to correct. This section shows the number of errors per application, how often they have occurred and other information about how they affect your system.


### Suggestions / Prioritization

In Coderr Premise and Coderr Live the "Suggestions" menu allows you to work with the errors that have the largest impact on your system. In this section, Coderr has prioritized errors based on different operational aspects. You can also add your own prioritization criteria based on your own business rules.

![](suggestions.png)

[How to configure prioritization](/features/partitions/)


### Search

The "search" menu option allows you to filter the error list using different options like tags, free text and incident state. Your last search is automatically used every time you visit the search page.

![](search.png)

The "Context collection" search option is quite powerful. Enter a user id to see how many errors a specific user has got. Requires that you have attached context data to your errors. [Read more](../client/manual-reporting/)


# Analyzing errors

Once you have assigned an incident to yourself, you can start to use the "Analyze" section of Coderr. It's designed to be able to help you understand why the error occurred. You can find all contextual information here, and the result of all built in analysis features.

To get started, click on "Analyze" and then use the second drop down to switch between your incidents.

![](analyze.png)

## Context information

Coderr includes context information out of the box.

![](context-data.gif)

But sometimes you might want to include information which is relevant to your application. 

You can either attach context data each time you call `Err.Report(ex, contextData)` or get it automatically included with every report by creating a [context collection provider](/client/extending/contextprovider/).

## Closing incidents

Use the "Close"-action when an incident has been corrected.

![](close-button.png)

Closing incidents tell Coderr to ignore all future error reports for the same error that are for same or older version of the application.

That requires that you use proper versioning in your application (`[major].[minor].[step/build]`).

![](close-dialog.png)

If the error resurfaces in newer versions, you will also be able to see how you solved it last time.

# Before going to production

Read this section carefully to configure Coderr correctly.

### Disabling Coderr's internal errors

When getting started with Coderr, it makes sense to allow Coderr to throw exceptions if the configuration is invalid or if reports can't be uploaded to the Coderr Server.

Once everything is OK, Coderr should not interfere with your application. Thus, you need to disable Coderr's own ability to throw exceptions.

```csharp
Err.Configuration.ThrowExceptions = false;
```

### Conditionally activate Coderr

The main purpose of Coderr is to identify errors in production environments. 

As a developer, you typically have full control of errors happening in developer environments. Thus it doesn't make sense to have Coderr  activated in development environments. 

To keep the error list clean, we recommend that you conditionally activate Coderr.
 
#### Conditionally activate Coderr in .NET 4.x

Add an app setting in your configuration file:

```xml
<appSettings>
   <add key="Environment" value="Production">
</appSettings>
```

Then check it when configuring Coderr (typically somewhere in `Program.cs`):

```csharp
if (ConfigurationManager.AppSettings["Environment"] == "Production")
{
    // This line is the one that activates the report uploads.
    Err.Configuration.Credentials("xxx");
}
```

#### Conditionally activate Coderr in .NET Core

Add an app setting in your configuration file (`appsettings.json`):

```json
{
  "Coderr": {
      "Activate": true
  },
  /*rest of the config */
  "ConnectionStrings": {
    "Db": "Data Source=.;Initial Catalog=Coderr14;Integrated Security=True;Connect Timeout=15;"
  },
}

```

Then check it when configuring Coderr (typically somewhere in `Startup.cs`):

```csharp
if (Configuration["Coderr:Activate"] == "true")
{
    // This line is the one that activates the report uploads.
    Err.Configuration.Credentials("xxx");
}
```

# Further readings

Don't hesitate to [email us](mailto:help@coderr.io) if you need help. Our [Guides and support](https://coderr.io/guides-and-support/) is otherwise a perfect place to visit next.