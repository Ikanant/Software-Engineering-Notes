01 - Introduction

Friday, April 29, 2016

12:09 PM

 

**What is Docker?**

Docker is a Lightweight, open, secure platform...

 

What Docker really is a tool that will help us simplify building, shipping and running applications in different environments... (Development, Staging, Production, etc)

 

Relies on \"images\" and \"containers\"

 

**What is an Image?**

Something that is used to build a container. The Image will have the necessary files to run something on an Operating System like Ubuntu or Windows.

The Image itself is not overly useful....it is more like a blueprint of getting a running container going...

 

**What is a Container?**

Where the live application run. Or the database...or whatever you are hosting

 

***Image:*** A read-only template composed of layered filesystems used to share common files and create Docker container instances

***Container:*** An isolated and secured shipping container created from an image that can be run, started, stopped, moved and deleted.

 

**Difference between Containers versus Virtual Machine?**

Virtual machines have a copy of full OSs for each Virtual Machine. Docker containers sit still on top of an OS, as well as using an Docker Engine.

Containers: Sit on top of the Host... Virtual Machines: Have their own copy of their files.

 

![Machine generated alternative text: Docker Containers Versus Virtual Machines App 1 Bins/Libs Guest OS App 2 Bins/Libs Guest OS App 1 Bins/Libs App 2 Bins/Libs Hypervisor Host Operating System Virtual Machines Docker Engine Host Operating System Docker Containers ](000_01_-_Introduction_000.png)

 

**Accelerate Developer Onboarding**

Often times we have multiple people working on a single project. We want people to work with the actual version of the app instead of other tools. Setting Servers, Databases etc can be challenging because of security, versions, and other elements of the application that can make it harder for a new developer to start coding. If we have these elements in Containers then the sharing of such elements will be much easier

 

**Eliminate App Conflict**

When having an app running on an specific version of a Framework running and want to update. Often time we CAN\'T because that might affect other application running on the Production Servers. Docker offers isolated containers that will have their own frameworks.

 

**Environment Consistency**

Development - Staging - Production

When working on multiple environments we can have major problem when switching between them. Sometimes our code works great on Development but breaks down when moved to the Staging environment because of lack of one or multiple requirements.

 

**Docker Tools**

-   Toolbox:

    -   Allows us to do a lot of the things we wanna do with images and containers (like building an image and running a container)

    -   It will require a Virtual Machine.

    -   Works on Windows, Mac and Linux

    -   **Docker Client**

        -   How to interact and view our images and containers

    -   **Docker Machine**

        -   Allow us to work with the Virtual Machine so the Docker client can interact with the different containers

    -   **Docker Compose**

        -   Allow to run Multiple containers. A simple way to have multiople containers talk to each other

    -   **Docker Kitematic**

        -   Allows us to locate Docker images out there without the use of the terminal through a cool GUI

    -   **Virtual Box**

        -   Allow us to host all the containers we will spin out
