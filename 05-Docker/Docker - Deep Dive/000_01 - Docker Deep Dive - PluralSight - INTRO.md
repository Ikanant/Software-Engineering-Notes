01 - Docker Deep Dive - PluralSight - INTRO

Friday, April 29, 2016

11:41 AM

 

Course taught by: *Nigel Poulton*

**The Ugly Virtual Machine**

Back in the day, whenever an application was going to be used in production, developers had to create the proper environment for such applications on physical machines. (In most cases there was a single app running in a single computer). This method was costly and unproductive. Commonly, applications would not even need to consume any relevant percentage of such machines and the result of such methods was an overwhelming waste of resources. So, what was the solution to such cases: Virtual machines.

With Virtual Machines, developers could use a single machine, create various different virtual machines within them and install single application in such environment. At first, developers were extremely satisfied with the results. Physical machines were able to handle multiple applications with minimal resource waste. But, was this the best solution ?

After much use, developers started to realize that the VM model was actually, kind of ugly. As much as Operating Systems are useful, developers had to step back and remember, we are using the OS to facilitate the use of APPLICATIONS. If we could spin out applications without the use of Operating Systems, we would. It would be great! Sadly the VM model, if we analyze it, it\'s all about the OS.....1 app per VM..... and each and every VM needs a full grown OS. Not so cool. Every OS needs all CPU, RAM and disk space. The VM model does nothing to optimize such arrangements. That even without counting that some operating system need individual licensing.

So, what is the most efficient solution to this problem? The answer is: The Container.

**What are Containers?**

Mega-High Level: Containers are a bit like virtual machines in the sense that they are application runtime environments. The difference with containers and virtual machines is that containers are WAY more lightweight. So each container, contains less CPU, less RAM and less Disk space than a VM.

![](000_01_-_Docker_Deep_Dive_-_PluralSight_-_INTRO_000.png){width="5.0in" height="2.183333333333333in"}

      

![](000_01_-_Docker_Deep_Dive_-_PluralSight_-_INTRO_001.png){width="5.0in" height="3.325in"}

In the VM model, inside each VM we need to install a full grown OS. So 10 VMs on a physical computer then that would be a lot of resource use. Refer to the picture above.

Containers are fundamentally different. Each container is a super lightweight OS. Nothing like the full grown OS. Every container shares a single Linux Kernel in the host. Even though we have lots of container running on it. Each and every container will consume a lot of less space. They will be faster and more portable than VM.

**Containers Under the Hood**

How come we need containers? Why don\'t we just install 5 different apps on top of our OS Linux or Windows? Well, Open systems OS are not good at isolation multiple apps and stopping them from running all over each other.

Example: Image two apps installed on an OS and share a same library file but each need a different version of that file. OS are not great at handling two different versions of the same file on the same system. There are many other reasons but we will see them later.

**Container:** Isolated instance of User Space

A system with 10 containers, has 10 instances of user space.

In order to achieve this, we need to be able to create our own isolated instances of things like:

\- Root File Systems

\- Process Trees

\- Networking Stacks

\- etc

What all this means is that, one container needs to have it\'s own view of a root file system:

![](000_01_-_Docker_Deep_Dive_-_PluralSight_-_INTRO_002.png){width="5.0in" height="2.65in"}

 

As shown in the picture above, containers will pretty much have their own file root system. What this means is that certain containers will have the freedom to modify in any way it\'s environment without necessarily affecting any of the other application running on the same OS. The same goes for the process tree or for the network stack. A process inside one container cannot send a signal to another process inside another container.

**Important Kernel Features:**

**Namespaces:**

How do we actually build this stuff? How do we achieve this isolation?

The answer is:** **Namespaces

Namespaces are a feature of the Linux Kernel. Kernel namespaces allow us to partition up system namespaces like:

\- The Pid Tree

\- The Process Tree

\- etc

and assign the partitions to one container and another isolated partition to another container.

From the view of the HOST, there is a single process tree.

Linux kernel namespaces allow us to partition various aspects of the system:

-   The Process Tree **pid**

-   Networking **net**

-   File systems and mounts **mnt**

-   User namespaces **user**

    -   In fact the user namespace allow us to have root privileges inside a container but NOT outside of the container

-   etc

**CGROUPS**

CGROUPS: Let us group together resources and apply limits. In the case of containers we map containers to CGROUPS in a 1-1 mapping, so basically a CGROUP equates to a container, and assign limits to how much CPU, memory, block IO that the container has access too. The CGROUP are really flexible, so we can tweek them as we write our app. CGROUP help us ensure that no single container can run a mock on a system and affect anything else on the system.

**Capabilities**

High-level: Capabilities give us high-grain control over what type of privileges a user or a process gets. So instead of all or nothing approach of granting root access or non-rootaccess to containers, Capabilities take those privileges of the root user and breaks them down into smaller privileges and assign them accordingly when and where we need them.

Assume we have a process that needs to be able to bind a socket to a low number port within a container, aside from that it doesn\'t need any other special privileges. Well, instead of granting it root and giving it way more privileges than it actually needs we can just give it the **CAP_NET_BIND_SERVICE** capability. Which is basically the capability to bind the socket on a privilege low socket port.

Socket supports Capabilities and all all denied by default. EXCEPT those that are listed within the **Whitelist.**

**Docker**

Both a COMPANY and a TECHNOLOGY (Platform)

At it\'s core, Docker is a container runtime

Docker is an actual implementation to a container technology. It groups all of the elements we have previously talked about into a product.

*[Author\'s personal analogy]{.underline}*

Docker is to Containers is what RedHat or Ubuntu is to the Linux Kernel. It is a packaged shipping implementation that you can get support for.

Docker provides a very uniform standard run-time. By run-time we mean an environment with the things that an application need in order to execute. Developers can code app on Docker containers on their laptop and literally drop them straight into Docker containers in Amazon Web Services, Corporate Data Centers, etc....as long as the destination has the Docker runtime or the Daemon.

Its a lot like writing an app for android. That app should work on any phone or any environment that is running Android.

Docker is evolving as a technology and its growing from just a container runtime. It is turning into a platform. (Docker\'s company used to be called dotCloud)

**The future of Docker**

Docker going to Windows (very soon). But, how could this be a standard runtime? Well we have to remember that when using the Docker runtime the containers will use the underneath Kernel installed of the machine. Meaning, let\'s assume we have two windows applications installed on a Windows based Docker runtime on top of a Windows operating system, if we install a Linux app, it will have a problem dealing with the kernel features that it needs. In many cases (commonly in labs or in initial steps for companies that adopt Docker) we can just have Docker runtimes on top of Virtual Machines...and even though this is not necessarily wrong, the author of this class thinks that in the future almost everyone will be dropping out of the VM structure and just have Linux on the bare root of the server. That way we have far better efficiency. At some point, AMD or Intel can even make chips that are meant to work better with Container Environment for the improvement of Efficiency and Security.

*Docker and Containers in general also tend to work best in micro services architectures. This is were applications are designed with a sweat of smaller services that collectively operate to run the app. Each of this smaller components services run as single process inside of their own containers. These containers and processes then communicate with each other to form the app. But, each component service (running on its own container remember) is individually upgradable and independent of all the other components of the overall application. This kind of application design seems to be the future of web application. Which seems to improve on the classic monolithic application, where upgrading any one component is a huge risky piece of work.*

**Installing Ubuntu Linux and CentOS Linux**

Linux Distros:

-   Ubuntu (we will work on this)

-   CentOS (we will point out where things are different)

-   CoreOS

-   Elementary OS (most beautiful)

-   openSUSE (best for laptops)

Remember that if we want the ultimate efficiency we would try to run Docker on a bare installation of Linux. But we have to understand that Docker works fine with Virtual Machines. So, let\'s begin\...

note: Docker only works on 64 bits architecture. Which is probably a good thing\...

**Installing Docker**

\$sudo su

This command will grant us sudo access for the rest of the session.

\$service docker.io status

Why do the need docker.io? Well, when creating the docker package, the developers ran into an existing tool within linux called Docker....so they had to rename their service accordingly.

*[Recall:]{.underline}* Docker is written in **GO** language (created by Google)

\$docker info

We will get some basic information including **Storage Driver**, which will be different between Ubuntu and CentOS.

-   Ubuntu: **AUFS**

-   CentOS: **devicemapper**

    -   CentOS does not use aufs mainly because AUFS isn\'t in the mainline of upstream kernel (and it\'s likely it will never be). RedHat policies are to only take from upstream.

 

This command will also show Execution Driver....which remember can be native (lip container) or LXC (which Docker didn\'t want to use it set them dependent of another product)

\$su - root

With CentOS, this command will grant us access to root access.

Install on Ubuntu

\- apt-get install docker.io

Install on Red Hat/CentOS

\- yum install docker

Basic Commands

\- docker -v

// Basic version info

\- docker version

// Shows more detailed version information

\- docker info

/\*

Number of containers

Number of images

Storage driver

Execution Driver

etc

\*/

**Updating Docker**

-   Make sure you back your data up before performing upgrades etc\...

-   Most of the time .... Containers/Docker are not an excuse to abandon best practices

Basic Commands

\- wget -qO- <https://get.docker.com/gpg> \| apt-key add -

// Add the docker repo key to our local apt key chain. That\'s where we are getting our new version on.

\- echo deb <http://get.docker.com/ubuntu> docker main \> /etc/apt/sources.list.d/docker.list

// Adds the Docker Repo to our apt sources.

\- apt-get update

// Sync to our new repo

\- apt-get install lxc-docker

// Let\'s check the latest version we can get now

**Granting Docker Control to non-root Users**

Docker needs root to work. It gots to do a lot of privileges action when dealing with new containers. So it needs root

By default: The Docker daemon listens on a local unix socket: docker.sock

Binds to /var/run/docker.dock

var/run is a link to run, so if we do

\- ls -l /run

We can see the docker socket there. The little S at the start of the line is what tells us that it is a socket. We can see that its bound by ROOT but, the GROUP OWNER on the second column is a group called Docker. So, instead of needing to be root to run Docker, we can add normal users to the Docker group...which has GROUP ownership of the socket. Effectively giving any users that amend to that group ROOT, because the DOCKER group has full control of the Docker UNIX socket.

In summary: *[We can grant normal users the ability to make and break containers without having to give them ROOT.]{.underline}* (no need of sudo anymore!).

**BUT:** Doing this is not without security concerns. We need to have strict control to know which users are within that group.

Basic Commands

\- exit

// If in ROOT to exit.

\- docker run -it ubuntu /bin/bash

// DENIED. On the unit socket.

\- cat /etc/group

// Make sure that the group exists

\- sudo gpasswd -a ikanant docker

// Add Ikanant to docker group

\- logout

// In order for our changes to take effect we need to logout and log back in. Once this is done we will retype the same denied command from before. This time it will work!

Notice that once this is effective we no longer have the same PS1 prompt. We are not logged in into the command line of our individual container. (as root). The number in front of @ it\'s the container unique ID.

\- exit

// Will exit the container all together.

**Configuring Docker to Communicate Over the Network**

So, what we are gonna do here is configure the docker daemon on our ubuntu host to listen on a  network port instead of a local unit socket. Then we are gonna connect to it from our CentOS machine.

// From Ubuntu

\- docker -v

// It results in 1.9 for me (NOW)

// From CentOS

\- docker -vdo

// It results in 1.8.2 for me (NOW)

// First let\'s show that we don\'t have Docker already listening on a network port

\- netstat -tlp

// Now let\'s stop Docker, and lets restart it but this time we will tell it to listen on the network instead.

\- service docker stop

// Now let\'s start it

\- docker -H 192.168.56.50:2375 -d &

-   2375: standard non-ssl docker port

-   -d: daemon mode

-   &: to give us our command prompt back

Things started to get a little confusing because \'-d\' is deprecated. I will only watch this tutorial.

**Playing Around with our FIRST Docker Container**

\- docker run -it centos /bin/bash

-   -it: Interactive

-   /bin/bash: Run the bash process

// After this step we are successfully inside the root of our container. A normal bash prompt in shell. We can ping stuff, for example: ping 8.8.8.8

 

\- ps -elf

// See what is running

\- cat /etc/hosts

// The first line will be our host name and our IP address. Notice how the host name matchers the PS1 prompt

So this example is a bit interesting. Right now we are using a CentOS container inside an Ubuntu machine. Is that right? 

\- uname -a

// From here we can see that we are sharing the same 3.13.0 kernel....it even says Ubuntu there. But if we look at:

\- cat /etc/redhat-release

\>CentOS Linux release 7.0.14.06 (Core)

// It definitely think is a CentOS 7 box.

// So, what if we use: apt-get update. Remember that apt-get update. apt is the package manager used by Ubuntu and not CentOS

\- apt-get update

// ERROR. As expected, it did not work.

// How about a yum check-update. yum is the red-hat and therefore the CentOS package manager\...

\- yum check-update

// WORKS

So in conclusion we are currently property using a CentOS container only sharing the Kernel of the host machine. What we are currently using is a container that is an Uber lightweight Linux  machine. So, quick question:

What happens to any data we write/save in our container?

Well, let\'s begin by creating a file:

\- vim /tmp/testfile

// Here we are getting an error because at the end of the day we are working on an Uber simplified linux machine. So, let\'s install it... easy

\- yum install vim

// Installing perfectly. Like a normal Linux machine

\- vim /tmp/testfile

\- cat /tmp/testfile

// Boom, it works great.

Now, what if we stop the container?

\- exit

\- docker ps

// No Docker containers running

\- docker ps -a

// We can see all containers that have been run on this machine. Including the host name we saw before. In this case: ff7f984c22e7

Let\'s check it out. Remember we are outside the container and that it is currently off.

\- ls -l /var/lib/docker/aufs/diff/

// We see a list of items and if we look carefully we can see one of the lines that starts with ff7f984c22e7. Let\'s go there\...

\- ls -l /var/lib/docker/aufs/diff/ff7f984c22e7..............

// This shows the machine and within it a tmp folder. Let\'s go in there\...

\- ls -l /var/lib/docker/aufs/diff/ff7f984c22e7............../tmp

// And there we go, the file that we created before is there. EVEN with the container not running.

Let\'s now spin that container back up and see if we can still see the file:

\- docker start ff7f984c22e7

\- docker attach ff7f984c22e7

\- cat /tmp/testfile

**Note:** Container names can be: **\[a-zA-Z0-9\_-\]**

**Note2:** With Centos, in order to stat the docker service we need to type:

\$sudo service docker start

![](000_01_-_Docker_Deep_Dive_-_PluralSight_-_INTRO_003.png){width="5.0in" height="2.7333333333333334in"}
