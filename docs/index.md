OneTrueError documentation
===============

Welcome to the OneTrueError documentation. 

The documentation have been divided into two sections:

# Client documentation

The client libraries are used in your own application to be able to detect and report exceptions.

The documentation focuses on usage, but also have a small section that shows how you can extend the client libraries and/or build your own for your favorite framework.

[Client documentation](client/index.md)

# Server documentation

The server documentation show how you can install and configure OpenTrueError Community Edition, which is the open source alternative to our hosted solution OneTrueError Live.

There is also a section that shows you can write your own plugins for the Community Edition and the OnPremise commercial alternative.

[Server documentation](server/index.md)

# OneTrueError pipeline

Below is an illustration that shows the OneTrueError pipeline.

It shows how an exception is handled from first detection to analyzing it in the server.
Do note that all analysis services typically subscribe on the `ReportAddedToIncident` event, thus all analyzers will be invoked
when the pipeline shown in the image ends.

![](pipeline.png)
