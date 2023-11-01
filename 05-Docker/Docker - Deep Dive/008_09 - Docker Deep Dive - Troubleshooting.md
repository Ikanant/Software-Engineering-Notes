09 - Docker Deep Dive - Troubleshooting

Friday, April 29, 2016

11:45 AM

Course taught by: *Nigel Poulton*

**Docker Daemon Logging**

Docker Daemon has a few different logging modes:

-   debug

-   info

-   error

-   fatal

\- service docker stop

// Before starting to set up the logger we need to exit the docker service

docker -d -l debug &

-   -d = Is to tell Docker the we want tos tart the damon. Rather than the stuff we have done before.

-   -l = Log level

-   & = Get our terminal back

\- docker ps

// Even this will show us what\'s going on back end.

So, in order to write down all the stuff onto a specific file we do a regular UNIX command like:

docker -d \>\> 2\>&1

We are not restricted to doing this way. We can add this option to the docker config file so they get picked up when we start the daemon from a script

\- vim /etc/default/docker

*Come all the way to the button and add our log level\...*

*DOCKER_OPTS="---log-level=fatal\"*

*Now let\'s kill the current docker rprocess*

*ps -ef \| grep docker*

// Here we can see the process running and interestingly containing the line with the parameters it was started with.

\- kill 1733

*We gonna start it up again, this time through it\'s service script\...*

*- service docker start*

***Container Logging***

Using the Docker log command we have already checked out the output from the PID1 process inside a container. Remember that, behind the scenes anything that PID1 inside a container writes to the Standard Out error stream the Docker Daemon harvest this and stores in a JSON file and stores in the file system of the Docker Host.

So

\- docker logs

also

\- docker logs - f

It will dynamically update the output as and when new entries are inserted to the file.

**Planning Image Builds**

As we have mentioned before, when creating new Images we should always use Docker files, BUT in many situations we want to test out and make sure everything is working before actually writing the file and building it multiple times. For these cases we should just start from scratch, create a Container and live do all the actions we will later write onto the Dockerfile.

Example:

\- docker run -it ---name test ubuntu:15.04 /bin/bash

// This would be similar to FROM ubuntu:15.04

\# ping 8.8.8.8

// oh damn, ping NOT found ... we need to install it and remember to include it in the Dockerfile

\# apt-get install -y iputils-ping

// Would be similar to RUN apt-get install -y iputils-ping

// ups, we got another error....we should do an update and remember to put it like that in the Dockerfile

\# apt-get update

\# apt-get install -y iputils-ping

// GOOD... now we create our Dockerfile accordingly

**Intermediate Images**

Let\'s say we ignore our previous suggestion and we went straight into creating our Dockerfile for our ping container image. But then we make a typo mistake in our Dockerfile\'

RUN apt-get install -y *[ping]*

Ok, so what happens is that we get an error half way through the build of our image....but let\'s remember something from a while ago...When creating an image from a Dockerfile, we Docker Daemon creates containers, commits images and then deletes the containers. In our case, we got an error BUT if we do 

\- docker images

We will see an image there that was created.....the cool thing is that THAT is the last image that was created from the Dockerfile before we got an error. So, this image is the PERFECT template to test what went wrong. In this example we are only dealing with a typo but in the future some of these errors might not be as obvious. We jus need to spin up a container based on this image and THERE... start testing\...

**The docker0 Bridge**

So, when the docker daemon starts, no the host machine, it does a bit of very basic network checking before it decides which network IP addresses to assign the docker0 bridge. So the docker damon knows exactly what IP addresses assign to which container. BUT, there will be time where we will explicitly tell which network address range to assign tot he bridge. This get\'s done when the daemon starts. For this, the cleanest way to do it now is by:

1.  Kill the docker service

    1.  service docker stop

2.  See current address

    1.  ip a

3.  Bring the link down

    1.  ip link del docker0

4.  Edit the docker config file

    1.  vim /etc/default/docker

    2.  DOCKER_OPTS=---bip=150.150.0.1/24

        1.  bip = Bridge IP

5.  Fire docker service back up

    1.  service docker start

6.  Check IP of the docker0

    1.  ip a

7.  Now, if we go and fire a container up

    1.  docker run -it ubuntu:15.04 /bin/bash

    2.  ip a

        1.  There we go. It worked

        2.  Any old container that we restart, its gonna assign it\'s new container.

**IPTables (Firewall configs)**

We are talking about the local IP tables firewall on the Docker Host. By default, docker allows all containers on the same docker host to freely communicate with each other. This ability for all containers on the same system for all containers to communicate its governed by a couple of parameters:

-   ---icc=

    -   Default to TRUE

    -   Inter Container Communication. Determines whether or nots containers can communicate with each other and the Docker Daemon

-   ---iptables=

    -   Default to TRUE

    -   Determines whether our Docker will make any modification to IP tables rules.

![](008_09_-_Docker_Deep_Dive_-_Troubleshooting_000.png)
