03 - Installing and Configuring Octopus Deploy

Thursday, November 17, 2016

8:49 PM

 

![Module Overview Install and configure the Octopus Deploy Server Create a QA and a Live environment Install Tentacles Connect deployment targets to the server ](002_03_-_Installing_and_Configuring_Octopus_Deploy_000.png){width="5.0in" height="2.4583333333333335in"}

 

 

For the application we will use for the Demo we will use:\
 

-   Window Server 2008 or Later

-   SQL Server (including Express and SQL Azure)

-   .NET framework 4.5 or later

 

1.  We will download the Server package for the Octopus component

    -   We run the MSI

    -   Indicate where Octopus Deploy will store it\'s data

    -   The Octopus Deploy Server runs as a Windows Server

        -   By default it runs under a local System account

    -   Indicate which Database to use

        -   Any MS SQL database will do (Including SQL Express)

        -   If the SQL server is not on the same machine and we need to use SQL Server Authentication

        -   Name the Database... If the database doesn\'t exist, Octopus will create that database for us

    -   To access the Server we will connect to a Web Portal

        -   The Web Portal is an embedded HTTP server

    -   Set the authentication process for future users of the server\
         

    -   After the Installation is finished it will automatically open the Octopus Manager

        -   Windows Client that allows you to configure the built in web server and several other settings.

        -   The only thing we want to do here is to make sure the Server is available from outside.

            -   **Change Binding**

                -   Add octopusdeploy.hernandez.net //whatever we want

                    -   In order for this to work we just need to make sure that the domain DNS has an A record pointing to the public IP of the server.

                    -   We also need to make sure the Firewall is allowed to receive incoming connections on port 80

    -   Now are DONE\
         

2.  The next thing is to Configure our Environments

    -   Because a Deployment Target is required to be in an Environment, we need the environment to be configured before we link the deployment targets to the server.

    -   To create an environment we need:

        -   Go to the Environment Tab

            -   Add Environment

                -   Provide Name and a Description for the Env.

                -   Guided Failure mode:

                    -   Means that we have ability to MANUALLY intervene if something goes wrong.

                    -   In QA we would want this to be OFF since we want our failures to propagate in our Testing Environment.

                    -   In the Live we do want to be able to check manually if something goes wrong when deploying to LIVE\
                         

3.  Link the Deployment Target to the Server

    -   Requirements

        -   .NET

            -   4.0 up to 3.1

            -   4.5 for 3.5+

    -   Similar to that of installing the Server, first we need to download the Octopus Tentacle MSI from the Octopus website

    -   Indicate where Octopus stores its configuration and log files & and default location where Octopus should deploy applications too.

    -   Define Communication

        -   **Listening Mode**: It will be the Server who talks to the Tentacle Agent.

            -   This mode is recommended because it tends to be faster and gives us more options in terms of security

        -   Polling Mode: It will be the Tentacle Agent the one asking for new commands periodically\
             

    -   Listening Mode:

        -   We need to make sure there is a listening PORT the server can connect to. We can leave this as standard (10933) and make sure the connection gets added as a firewall exception.

        -   For security reasons a tentacle will only receive commands from a server it knows

            -   The Server has a THUMBPRINT that we need to specify here

                -   To get the THUMBPRINT we need to:

                    -   Get into Configurations

                    -   Certificates

                -   We need to copy that value and pass it to the tentacle

    -   Once the tentacle is ready and listening to commands from the server we can now ADD it as a deployment Target.

        -   From the Environment Tab, we will add a deployment Target to the QA environment and we will add it as a listening tentacle. Since the server needs to connect to the Tentacle we need to ADD in the HOST name.

            -   In this case we will set the Hostname to be 10.0.0.5 and the PORT will be the same we chose for our tentacle: 10933

            -   Once we click DISCOVER, the server will attempt to make a connection with our created tentacle

 

-   Once verified we will proceed to configure the deployment target:

    -   Name: (we name it whatever we want)

    -   Environment we want to add it too. (We can add to multiple environments)

    -   Roles: Roles are simply TAGs we can attach to a deployment Target. They will be used to direct our deployments to certain targets.

        -   Example: Web-server & Web-service

>  
>
>  

 

 

>  

 
