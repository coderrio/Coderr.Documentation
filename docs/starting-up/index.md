Starting up
===========

Here is a description of the steps you will go through when starting up codeRR for the first time. You begin by registering and creating an account followed by logging in and making sure you can see monitor your application in codeRR. Registering and creating an account only needs to happen once, so the second time you are using codeRR, you will get straight to the log-in page after signing in.

Below you will find a series of instructions and screenshots intended as a guide to have if something goes wrong or you need to pause the process and then return later. If you find anything not working during this process, please email us at help@coderr.io so we can promptly assist you. We might also email you if we notice you have not completed all the steps.

# 1. Registration

You can use either an existing external account (choice on the left) when registering or creating a new account specifically for codeRR (choice to the right). Next time you are using codeRR, this is the view that you will see again, so please remember your sign-in details.

![](register-first-page.png)

If you are registering using an external provider account (to the left) then you will need to finalize your registration in the following window. Note that you can sign in with a different username than what you used for authentication. The user name that you put in will be the one you register. 

![](register.png)

If you are creating a new account (option right) and have clicked the blue "Register" - button, your input is needed to finalize registration in this window:
 
 ![](register-local.png)

# 2. Creating an organizational account

As codeRR is intended to be used by organizations with multiple users, you will need to associate your registration with an organization. The future billing is linked to that organization. You either join the already created organization (click "join") or if you are the first from your organization, you will create a new account (click "create").
 
![](welcome.png)

The only way to join an existing organization is to receive an invitation email from a colleague. The "Join" page will just inform you of that fact.
 
If you clicked "Create" earlier, you can fill in you the name of your organization or company (here shown as the test name "Acme Inc.") and then click "Create" once more to associate your registration with an organization. 

![](create-org.png)

codeRR is now setting up your database and your account. 

After successfully creating a new organization, you will receive a welcome email from us, confirming your registration.

# 3. Logging in

If you successfully have completed step 1 and 2 above, then you will reach the "Login"- screen. This is also the view you will see when returning to codeRR next time. From here you normally would just be  logging in to the organization that has been associated with you (shown as "mix max" in the example).  If you are the first to register your organization with administrative privileges and you have multiple organizations, you can log it to those here. you can remain associated with the named organization. You can also activate your subscription at any time.

![](login-org.png)

# 4. Creating an application

You need to identify the error reporting entity and name the application that you want to monitor. Write the name of your application and then click "Create". For clarity we recommend that you name your client and server as two different entities (or applications). That way it is easier to see where the error has been generated. If you later would like to add another application to codeRR, you can do it from this window.

![](create-app.png)

# 5. Configuring your application

Select the correct .NET library or framework that you have used in your application and click "Configure". 

![](configure-app.png)

You will now see a set of instructions that you will need to follow. First, ensure you have installed the related nuget package of your chosen .NET library. Next, you need to see to that the codeRR library knows what server to upload the errors to. The further instructions show how by adding lines of code, you configure where you want the errors reported to. There is also an example of how you set up automatic reporting.  

After adding the lines of code, test your configuration by trying to produce an error manually. In your application, add a piece of test code and invoke your controller action. After successfully generating an error (see below) you can delete this line of code.
Click "Configuration is done".

```csharp
var url = new Uri("https://report.coderr.io/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");

``` 
     

# 6.	First error generated

If you have been successful with testing your configuration by generating an exception you will see it here in codeRR. Please now go to [Reporting Errors](https://coderr.io/documentation) on our website for more information about how to work with codeRR.

![](reported.png) 

In case codeRR could not see the attempted exception, please contact us at [help@coderr.io](help@coderr.io) so that we can assist and investigate what went wrong. 
