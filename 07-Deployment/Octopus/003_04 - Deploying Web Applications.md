04 - Deploying Web Applications

Friday, November 18, 2016

9:47 AM

![](003_04_-_Deploying_Web_Applications_000.png)

**Create a Project**

1.  **Head over to the PROJECT Tab and click ADD PROJEC T**

    a.  Name: (whatever we want)

    b.  Description ...

    c.  Project group: Meant for organize our projects

    d.  Lifecycle: Determines how we are going to move a release from ONE environment to ANOTHER. The DEFAULT option specifies that an application needs to be deployed first to QA and only then to LIVE.

2.  **In the PROJECT OVERVIEW page we will see:**

    a.  Overview

    b.  Process: Define the steps for deployment

    c.  Variables: Set custom variables for our application deployment process

    d.  Channels: Allow us to manage different types of Deployments such as BUG fixes and FEATURE releases (NOT COVERED IN THIS NOTES)

    e.  Releases: We can see all the releases created for this project

    f.  Settings: Change same settings we configured when creating this project

3.  **First we need to specify how this project will be deployed. We head to the Process Tab:**

    a.  Here we can add steps to our deployment process. For now we will only have ONE step (deploy a package)

        i.  Name

        ii. Role... this will specify that this process will run on every deployment target that have that role attached to them.

        iii. Package ID (we don\'t have it yet but we will create it later with the name of our example application)

        iv. Configure Features

            1.  Here is where we will need to select the IIS web site and Application feature.

                a.  We will be greeted with some familiar settings: This settings are the ones that will be applied to IIS when we deploy a package. Octopus deploy will automatically set the correct HOME directory of the website of where the Package was deployed too.

                b.  Configure some settings ourselves:

                    i.  Web Site Name

                    ii. Binding:

                        -   Protocol

                        -   Port

                        -   IP Address

                        -   Host Name: ex qa.todo.hernandez.net

                    iii. Authentication modes:

                         -   Anonymous since our application has its own authentication system.

                    iv. Set Octopus to ONLY run this step in selected Environments

        v.  Now that we have the Project Created and Defined how it should be deployed, we need a RELEASE to deploy.... BUT before we can do this however, we first need a package from which we can create a release.

4.  Create Public Packages

![](003_04_-_Deploying_Web_Applications_001.png)

**Options for creating Public Packages:**

1.  Since NuGet Packages are essentially ZIP files... we could create them manually or use the NuGet package explorer application. We could then upload them directly to the Octopus Deployment Server...

    a.  This is not a good option as it defeats the purpose of an automated pipeline.

2.  NuGet.exe

    a.  This will also requried some extra steps to make sure our package is correctly packaged up

3.  Octo.exe

    a.  Command line tool built on top of the octopus HTTP API

    b.  It contains commands for packaging and containing NuGet packages.

    c.  This is a tool we would use for NON-.NET applications.

```{=html}
<!-- -->
```
4.  **OctoPack**

    a.  NuGet package itself

    b.  When we install it into the project we want to deploy, it will add an MS build task that will allow us to create and publish our packages

![](003_04_-_Deploying_Web_Applications_002.png)

>  

5.  **Create and Push a Package**

    -   ![](003_04_-_Deploying_Web_Applications_003.png)

>  

-   Keep in mind that in order to push a package to the Octo Server we will need an API key.

    -   We can generate an API key from the Portal by going to Profile \> API Keys \> New API Key

    -   Beware that these API key is hatched inside the Octo Database and cannot be retrieved.. Make sure to NOT lose it

-   ![](003_04_-_Deploying_Web_Applications_004.png)

6.  **Create and Deploy a Release**

    -   **We can create a RELEASE from the Project Home Page \> Releases**

        1.  Specify version and release notes

            -   Remember that the Version and the Release notes are different from those of the package

            -   The package only contains Source Code while the RELEASE holds all our settings such as the steps and the variables PLUS a package.

        2.  Once the RELEASE is created we can head over the OVERVIEW tab and see that our new Release is ready for Deployment.

        3.  Deploy to QA:

            -   The TASK Summary will show you the high level overview of the steps. Here we can see that the package is sent to the deployment Targets and then our STEPS are executed

            -   The TASK Logs provide us with a more detailed overview

        4.  Now that the Deploy is NOW finished... let\'s head to the DEPLOYMENT TARGET and see what has happened:

            -   ![](003_04_-_Deploying_Web_Applications_005.png)

-   In the Directory we can see that a Package was SAVED. This is done so that later deployments of the SAME package DON\'T need to send the same package again.

-   Also on the Applications Directory we can see that our application was unpacked. In IIS we can see that a new website was created and it\'s physical PATH is pointing to the Deployed Web App.

    -   It is also using the Newly created Application Pool

5.  Now that the Deployment process in QA was successful we can now repeat the same process on LIVE environment.

>  

![](003_04_-_Deploying_Web_Applications_006.png)
