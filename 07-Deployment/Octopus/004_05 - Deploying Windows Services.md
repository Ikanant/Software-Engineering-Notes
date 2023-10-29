05 - Deploying Windows Services

Friday, November 18, 2016

11:02 AM

 

The Process to accomplish this step is LARGELY similar to what we did for our previous WEB application.

 

 

![](004_05_-_Deploying_Windows_Services_000.png)

 

 

1.  We start off again by creating a Project & adding a package deployment STEP to it.

    a.  This package will be deployed to all Deployment Targets that have the role \"Windows-Server\" on them

    b.  For this project the Package ID will be : TODO-Service

2.  Just as we added a feature for deploying web applications using IIS in our previous step, this time we will do the same but select: WNDOWS SERVICE

3.  Specify General Info

    a.  Name

    b.  Display Name

    c.  Description

    d.  Path to the Executable to Run as a Service as well as any potential arguments I want to pass in for startups

    e.  Start Mode

4.  With the Project done (the Service) we need to package it into a NuGet package

    a.  After creating the package we will run the msbuild from the Command Line to Package the application and PUSH it to Octopus Deploy

    b.  ![](004_05_-_Deploying_Windows_Services_001.png)

5.  Create a Release

    a.  We will use the same versioning Scheme we used for our previous Application

6.  Now we can install the package into the QA environment

    a.  Once install is done we can go into the logs to check that everything has been done correctly and that the service has been started successfully

    b.  To Verify:

        i.  We can have a look at the Server where it was installed. Here we can see that the application binaries have been copied to the octopus application folder:

            -   ![](004_05_-_Deploying_Windows_Services_002.png)

        ii. If we look at the Services we can also see what\'s going on there

            -   ![](004_05_-_Deploying_Windows_Services_003.png)

7.  Since the Deployment to QA was successful we can do the same for the LIVE environment.
