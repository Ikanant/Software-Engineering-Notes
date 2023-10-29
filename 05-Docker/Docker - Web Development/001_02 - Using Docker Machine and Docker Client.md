02 - Using Docker Machine and Docker Client

Friday, April 29, 2016

12:11 PM

 

Docker machine will be used to create and manage our local machines or cloud machines such as ones in AWS or AZURE. It will also configure Docker Client to talk to Machines.

 

Commands:

-   docker-machine ls

    -   List all different machines that we can issue docker commands against

-   docker-machine start \[machine name\]

-   docker-machine stop \[machine name\]

-   docker-machine env \[machine name\]

    -   This will setup the environemnt for the given machine name. For example...if we open a new terminal windows and try to run a docker command on a machine (RUNNING) it might say it is not connected to that machine....for that then we just run this command and it will set evertyhing up for us.

-   docker-machine ip \[machine name\]

-   docker-machine

    -   List all commands:

        -   ...

        -   Create

        -   Inspect

        -   Restart

        -   Upgrade

        -   ...

 

**Getting Started with Docker Client**

The Docker Client is a tool that interacts with the Docker Daemon...

Docker Daemon: The Engine that can control the containers that are running.

\--\> Docker client will let us work with Images and convert those images to running containers

 

Commands:

-   docker pull \[image name\]

    -   Download Image from Dockerhub

-   docker run \[image name\]

-   docker images

-   docker ps

    -   List all containers
