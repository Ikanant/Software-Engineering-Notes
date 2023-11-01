04 - Docker Deep Dive - Container Management

Friday, April 29, 2016

11:44 AM

Course taught by: *Nigel Poulton*

**Starting and Stopping Containers**

*So, we know that containers are kind of Linux machines. Each one gets it\'s on own:*

-   *File system*

-   *Network environment*

-   *Process tree*

*All the good stuff that makes it a standard Linux runtime environment for apps to execute in.*

*Just like Linux machines, containers can be started, stopped and restarted.*

*We use the terminology, \*start\* a container, NOT boot a container.*

*- docker run -it ubuntu:14.04 /bin/bash*

*If we want to exit the container WITHOUT stopping it, we press:*

*CTRL+P+Q*

We call this, detaching from our containers

\- docker ps

We see the container still running

\- docker stop

Behind the scenes, the Docker Stop command sends a SIGTERM signal to the process with PID1 running inside of the container. **That is the process we tell the container to run at the end of the docker run command: /bin/bash (for now).** As a result the container itself will terminate.

\- docker kill

This will kill the container in a more brute force way. It will send SIGKILL.

\- docker kill -s

We can specify any process signal to 

\- docker ps -l

This will show us the latest container that was read.

\- docker start

Will start the container

\- docker attach

We will get back to where we started.

\- docker restart

Will restart the container.

**The "docker attach" command will attach to the PID1 inside of the container**

**PID1 and Containers**

Note: Anyone that is familiar with UNIX but hasn\'t necessarily worked with containers (ME) is probably confused with the PID1.

PID1 = **Is the process that we specify at the end of the Docker RUN command.** We have been doing /bin/bash so far.

Even though we have used /bin/bash a lot, the PID1 will usually that command will be something more like a command to start an app daemon.

BUT, in the NORMAL Unix world, **PID 1** is a special uber process called **init**.

**PID 1** or **init**: Is the mother of all processes. All other processes trace their relative history back to **init**. Meaning that ALL processes are forked from init, or a child of init. As the mother of all processes, **init\'s** got a few special jobs:

**init takes care of all of the processes of the system.** So, when PID 1 receives a signal to terminate, it makes sure that all the processes on the system are cleaned up as gratefully as possible. Ensuring, not only a graceful shutdown of init itself, but also all other processes on the system.

BUT, PID 1 in our container IS NOT **init**. For us it\'s been the bash shell, and for most production containers its going to be an app process: MongoDB, NodeJS, etc...These guys aren\'t designed to be init processes. They are not really designed to sit at PID1. For starters there is absolutely NO guarantee, that upon receiving a SIG term these guys will signal ANY of the processes in the container. The app process itself might catch the SIG term and handle it gracefully, but any other processes in the container they are going to be blamefully ignorant of the fact that the container is about to do a hard stop. NOT IDEAL

.....but (again), didn\'t we say we only run a single process inside of a container? Yeah, we did. And this is actually one of the major reasons why. But, there is actually no reason why we can\'t run multiple processes inside of a container. It can be done. In fact, there are docker images out there that are handcrafted to make life easier running multiple processes in a container. Some of them even give us a real **init** process inside of a container: SSH daemons, Chrome daemons Syslogs. Running gracefully inside of a single container. Doing this DOES violates what is almost a CORE term of Docker: **One process per Container.** And therefore, one concern per container. Lean and simple.

**Deleting Containers**

The Docker hosts keeps versions of stopped containers and their state somewhere on local storage.

\- docker ps

// Shows running container

\- docker info

// Look at Containers and Images stored in the Docker host

\- ls -l /var/lib/docker/contaners

// This is where can see all containers

\- docker rm

// This will remove the container. BUT, we can\'t remove any running containers, not with a bit of effort.

\- docker stop

\- docker rm

Remove means: DELETE. It\'s gone. Forever

If we want to brute force a removal for a running container we can just type:

\- docker rm -f

// We will use the -f flag

*[Cool Note:]*

 So far we can conclude that we are using docker ps A LOT...so, we can consider using some **shell aliases**

**---\>** For docker ps, in bash on our docker host we can type:

\- alias dps="docker ps\"

Now, if we type dps: AWESOME.

**Looking Inside Containers**

Earlier we used the: docker top to pick inside of a container. That is a good way of seeing what processes are running inside of a container from the outside. So we can be outside on our docker host and check what process is running inside any docker containers. 

So, if we take a look at a running container that has more than one process, if we type: docker top we will get a list of processes running. In the case of our example we are taking look at one container based on an almost full blown Ubuntu VM. We even see an init process running. (It is not the same as a regular init though). If we take a look at the IDs of such processes we see that they are all high level numbers (2040....2053)..... Now, that is if we look at them from outside the container and within our docker host. Now let\'s try:

\- docker attach

\- ps -ef

// There we go, we see all same processes but this time their IDs are much lower.

[Good Reminder about Namespaces:]

From WITHIN out container we have a fully isolated sandbox process tree. As far as the container is concerned, there is nothing outside it\'s process tree. It gas no concept of the Docker host itself and it only knows about it small partition area.

\- docker logs

// Will show everything happening inside of the container.

**Low-level Container Info**

\- docker inspect or

// Will return JSON structured text

The kind of info returned is very similar for Container and Images... This should be of no surprise since Containers are no more than running instances of Images.

The inspect command will return:

-   State of the container

    -   Running

    -   State

    -   Time that it was started

-   Basic Networking Info

    -   Container IP Address

    -   All container get a 16 bit subset mass

    -   MAC Address

-   The ID of the image it is based of

-   HOST config stuff

-   Execution Driver

Point is that -Docker inspect- give us great low level info about our containers

**Getting a Shell in a Container**

Running - Docker attach will attach our HOST terminal to the standard stream of PID 1 inside the container and that is fine if the process for PID1 is a shell (which it has been so far). That is not common in the real world though. In the real world most containers will be running proper applications. If we are running an apache web service lets say, attaching our terminal to PID1 inside of that container is not going to give us a nice friendly shell to work on. Docker Attach is not always the best way then\...

How about SSH? Well, running SSH inside of the container (as mentioned before) it\'s looked down upon. It can make things messy.

*[nsenter]*

-   Allows us to enter Namespaces

-   Requires the containers PID. (NOT the container\'s ID we have been working on so far, or their name...NO, nester needs the container PID). Where can we find that?

    -   We can get *[docker inspect]*

    -   docker inspect \| grep Pid

        -   Let\'s say it returns: 1923

-   nester -m -u -n- p -i -t 1923 /bin/bash

    -   m: Mount namespace

    -   u: Uts namespace

    -   n: Network namespace

    -   p: Process namespace

    -   i: IPC namespace

    -   t: Target

    -   /bin/bash to get a shell inside the container

Nice! but this is NOT the same as an attach.Because we are not attached to the standard streams of the containers PID1 if we do an EXIT, it actually logs us off BUT  it doesn\'t kill the container. The container will keep running.

*[docker-enter]*

-   Similar as before......if we EXIT, the container will keep running

*[docker exec -it /bin/bash]*

-   This is probably the RECOMMENDED way to get a terminal inside of the container

![](003_04_-_Docker_Deep_Dive_-_Container_Management_000.png)
