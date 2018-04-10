Partitions
===========

Partitions are used to segment incidents to be able to better prioritize which incidents to correct next.

A typical usage is to be able to tell the impact what each incident have on your system or users.

![](../screens/suggestions.png)

In the above example we have specified that we have 50 users in the system and Coderr is therefore able to tell that this specific incident affect 5% of our users.

We have also said that we have three database servers and can therefore see that the invalid SQL statement have only been reported from one of them.

# Adding partitions to incidents

The minimal configuration is to attach partitions to each reported incident.

In the following example we want to prioritize errors based on how many installations and users that each incident affects.

To do that we add the following configuration to our code:

```csharp
Err.Configuration.AddPartition(context => 
{
  context.AddPartition("InstallId", ConfigurationManager.AppSetting["InstallId"]);
  context.AddPartition("UserName", Thread.CurrentPrincipal.Identity.Name);
});
```

That's everything required. Report an error to see the information under the reported incident. 

You can also go to "My incidents" in the left menu to see suggestions based on your configured partitions.


# Improving suggestions

***You need to be an administrator to be able to make this configuration.***

When you have completed the configuration above, Coderr have no knowledge about the number of installations or the number of users.

Therefore, prioritization of incidents are made upon the known total (i.e. based on all distinct values that we have received so far for all incidents).

If you would like to know see the impact based on the actual number of installations or users you need to go to the administration pages and specify those.

1. Click on the cog in the top right menu<br>![](configure1.png)
2. Make sure that the correct application is selected in the top left menu<br>![](configure2.png)
3. Click on prioritization in the menu<br>![](configure3.png)
4. Click on "Create new"<br> ![](configure4.png)

Fill in the information about your partition.

Here is a sample for users:

![](configure5.png)

Once done, try to report an exception and then click on "Suggestions" under the "Discover" menu.