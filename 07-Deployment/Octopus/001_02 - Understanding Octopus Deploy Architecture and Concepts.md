02 - Understanding Octopus Deploy Architecture and Concepts

Thursday, November 17, 2016

4:53 PM

 

 

First let\'s analyze the Physical Architecture used with Octopus Deploy:

![p hysical Octopus Deploy Server SQL Database O Architecture Deployment Targets Tentacle O O O O Calamari ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_000.png){width="6.0in" height="3.425in"}

 

 

At the Core of the Octopus Architecture sits the Deploy Server:

 

-   **Octopus Deploy Server**

    -   Hosts the Dashboard

        -   Allows us to define logical components and applications

        -   To Store this data it relies on a **SQL Database**.

    -   Holds ALL packages of our software inside a NuGet feed

    -   Hosts the Windows Service that will send commands to the deployment targets:

        -   **Deployment Targets:**

            -   Machines in which we will install our applications

            -   Deployment Targets can be in any kind of Network environment as long as they can be accessed by the Central Server

            -   It contains **2** different components:

                1.  Tentacle

                    i.  Lightweight Windows Service which manages the communication with the Central Server. There are many ways of communicating but the *recommended* approach is **PUSH** communication

                        -   In **PUSH** mode: The tentacle listens to the commands from the Central Service. Once it receives the command it will PASS the command to a console application called CALAMARI

                2.  Calamari

                    i.  Knows how to deploy packages, run scripts and a bunch of other deployment related tasks

            -   The reason why these two components are split out is so that the Smart component (which knows how to execute commands - calamari) Can be easily updated from the Central Service. Since the tentacle is essentially a dumb communication component that will hardly need any updates

 

 

**Logical Concepts**

 

![Environments Projects Logical Concepts Web Services Roles Releases Deployments ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_001.png){width="6.0in" height="3.575in"}

 

-   **Environments**

    -   A dev-test / live separation is common but we can create any number of environments we like.

-   **Roles**

    -   This is how we designate roles to physical machines. This allows us to think in abstract modes instead of IT pieces and machines.

-   **Packages**

    -   When we want to deploy an application we need a package that contains everything we need. For this we will look into how Octopus deploy uses the concept of NuGet packages

-   **Project**

    -   Heart of our system. They will define how to deploy packages

-   **Release**

    -   Combination of Steps and packages to deploy.

-   **Deployments**

    -   The deployments is when we combine all of the above to deploy our code in one or more machines

 

 

![Environments Deployment Target Deployment Target Deployment Target Deployment Target ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_002.png){width="6.0in" height="3.225in"}

 

Normally when we deploy software we think about which files are going to which machines. While this is necessary it doesn\'t necessary coincide with what we think about deployments. We rather deploy something directly to Dev QA or Live.... That\'s why Octopus Deploy allow us to group deployment targets into environments. **Notice** that the deployment target can be attached to multiple environments but for simplicity sake our example will show us using only ONE environment.

 

![Roles QA WEB Deployment Target Services Deployment Target LIVE WEB Deployment Target Services Deployment Target ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_003.png){width="6.0in" height="3.566666666666667in"}

 

Apart from the Environment the machine belongs too, the machine usually also has a role. To avoid having to think about physical machines Octopus Deploy allow us to define Roles to Physical Machines. This allow us to add more physical machines when necessary without affecting the deployment process.

 

It meant for loose coupling between our physical architecture and logical deployments. A machine can have MULTIPLE roles and a single role can be applied to MULTIPLE machines.

 

For our example we will only do a ONE to ONE relationship. We will assign the WEB role in the machine in QA and the machine in LIVE and a do the same for the SERVICE role.

 

Environments and roles are the target to destinations we deploy too. Packages on the other hand are the BASIC building blocks from which we deploy from.

 

![Packages Collection of - DLL\'s Assets - Scripts NuGet ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_004.png){width="6.0in" height="5.116666666666666in"}

 

**Note:** This has no relationship as of how NuGet packages are used in development. It simply uses the distribution and packaging methods.

 

 

![Projects Recipe Definition of how software is deployed Deploy Package Notify Users Run Smoke Tests ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_005.png){width="6.0in" height="3.5in"}

 

A project has a ONE to ONE relationship with an application. A project is like a recipe for deployment. Is the definition of all the steps that need to be taken to deploy our software or (project)

 

An example of a Project can be:

-   Deploy a package

-   Notify the users that a deployment has been made

-   Triggering a Smoke test

 

 

![Releases Combination - Package - Project steps and settings ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_006.png){width="6.0in" height="3.841666666666667in"}

 

Releases will TIGHT together Packages and Projects. When we create a release it is IMPORTANT that the release is READ ONLY. So whenever Octopus Deploy creates a Release, it takes a Snapshot of all the steps and settings from the project and package of source code. This bundle can then be deployed atomically. This process will guarantee us that the deployment of a release will always yield the same result.

 

![Deployments Releases Steps Package Package Steps Role ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_007.png){width="6.0in" height="4.333333333333333in"}

 

When we deploy a project into an environment we pick a RELEASE to deploy. This release consists of one or more packages and a series of steps. The steps will define will package needs to be deployed to which role in the selected environment.

 

**DEMO:**

 

![Environments Environments 10.0.0.5 10.0.o.7 10.0.0.6 wiruiows service 10.0.0.8 wirxiows service Dashboard Roles Projects Library Tasks Edit Edit Kenneth Reorder Accounts Configuration Add environment Check health Check health Add deployment target Add deployment target ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_008.png){width="6.0in" height="2.9166666666666665in"}

 

 

![Environments Todo.Web Process Todo.Web Create release Overview Variables Channels Releases Settings Dashboard Deployment process 1• Deploy site Projects Library web server Tasks Kenneth Configuration Deploy package Todo.Web from Octopus Server (built-in) to machines in roles: Add step One Step defined Project Lifecycle Default Lifecycle R) QA C) Live Choose a different lifecycle This lifecycle defines how releases can be promoted between environments. Lifecycles can be defined in the Library. This the default lifecycle for the project. It can be overridden by specifying Channels, Automatic Release Creation C) Create a release when a package is pushed to the built-in package repository Script modules Include script modules The Library includes PowerShell script modules tha an ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_009.png){width="6.0in" height="3.191666666666667in"}

 

 

![Dashboard Environments Projects Library Tasks Kenneth Configuration Todo.Web Releases Todo.Web Create release Overview Process Variables Channels Releases Settings Releases All channels 1.0.3 Assembled Tuesday, March 29, 2016 1:04 AM Added title 1.0.2 Assembled Tuesday, March 22, 2016 12:55 AM 1.0.1 Assembled Tuesday, March 22, 2016 1253 AM Assembled Tuesday, March 22, 2016 12:32 AM We need to give it a Version number and select a package we want to include in this release. ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_010.png){width="6.0in" height="3.0416666666666665in"}

 

 

![1.0.4 Most recent release: Todo.Web Overview Process Variables Channels Releases Settings Create release Version Packages Step Deploy site Release notes Don\'t need to match Enter a unique version number for this release with at least two parts. See examples. Package Todo.Web Latest @ I.o.o.3 Last o I.o.o.3 Specific O Search Enter a summary of what has changed in this release, such as which features were added and which bugs were fixed. These notes will be shown on the release page. You can edit these notes later, Save ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_011.png){width="6.0in" height="3.3833333333333333in"}

 

![Projects Todo.Web Todo.Web Create release Process Variables Channels Settings 1.0.4 1.0.3 1.0.2 Dashboard Deploy 1.0.3 1.0.2 2016 Environments Live Library Tasks Kenneth Configuration 1.0.3 Mere 1.0.2 Mare 2016 When I click the deploy button it will deploy package 1.0.0.3 because it is part of release 1.0.4. To all the machine with the role WebServer that belong to the QA environment. ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_012.png){width="6.0in" height="3.216666666666667in"}

 

 

This is how Octopus Deploy tights all the concepts together so we can deploy with a high level overview instead of having to think of pushing files to machines.

 

 

 

**Summary**

 

![Summary Physical Architecture - Central Server - Deployment Targets Tentacles Calamari Logical Concepts - Environments - Roles - Projects - Packages - Releases - Deployments ](001_02_-_Understanding_Octopus_Deploy_Architecture_and_Concepts_013.png){width="6.0in" height="4.091666666666667in"}

 
