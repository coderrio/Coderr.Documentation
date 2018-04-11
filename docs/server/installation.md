Installation
==============

1. Start by [downloading](https://github.com/coderrapp/Coderr.Server/releases) the latest release.
2. Unzip it
3. Open IIS management console
4. Create a new application in IIS<br> 
 ![](install-iis-application.png)<br>
 ![](install-iis-new-application-dialog.png)
5. Copy the files to the new IIS folder.
6. Create a new empty database in SQL Server (for instance named `Coderr`).
7. Change the `ConfigurationKey` in `web.config` to your own value
8. Modify the connection string in `web.config` so that it contains the name of your database.
9. Open a browser and visit http://yourserver/coderr
10. Follow the online installation guide


## Troubleshooting

Get a blank page from IIS?

* Make sure that "Static Content" is enabled as a feature
* ASP.NET 4.5 must be installed
