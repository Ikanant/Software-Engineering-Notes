02 - Docker Deep Dive - Major Docker Components

Friday, April 29, 2016

11:43 AM

 

Course taught by: *Nigel Poulton*

**Module Outline**

-   Docker Engine

-   Images

-   Containers

-   Registries and Repositories

**THE BIG PICTURE (analogy)**

Let\'s grab a quick high level picture before diving into the details of each components. It\'s far from a perfect analogy, but it might make things easier.

Let\'s compare things to: a CONTAINER SHIPPING YARD

**Docker Engine: a.k.a. Docker Daemon, or Docker Runtime**

Docker Engine = Shipping Yard

Docker Images = Manifests

Docker Containers = Shipping Containers

![](001_02_-_Docker_Deep_Dive_-_Major_Docker_Components_000.png)

 

![](001_02_-_Docker_Deep_Dive_-_Major_Docker_Components_001.png)

 

**The Docker Engine**

This is simply the Docker program that we install in each Docker host to provide us with a Docker environment and access to all Docker services. The kicker to all this process is that the Docker Engine is standardized. So it looks exactly the same from one host to another (very efficient).

Standardized Runtime environment that looks and feels the same no matter where it is. Which makes everything extremely simple.

**Images**

Going from the very HIGH-LEVEL analogy from before, Images are like shipping manifests. Containing a list of everything that is in our container and instructions into how to build it.

Docker images is what we run Docker containers from. In order to launch a container we need an image. We used this earlier with the Docker run command. Let\'s do it again:

\- docker run -it fedora /bin/bash

-   -it: Make it interactive and give it a terminal

-   /bin/bash: Run a shell inside again

-   **fedora:** This is telling us which IMAGE to base our container on. So, this container will be based on a fedora image. Meaning: It will run a fedora OS. If ww don\'t specify an image we can run a container. If we type Ubuntu, well, we will run an Ubuntu based container.

So, Images are a bit like templates in the Virtual Machine World.

Images are comprised of multiple layers. For the Fedora containers, we see how three things get downloaded...and all of them show a specific ID on the left of the screen. This is a topic we will cover in the future but for now we can confirm that those three numbers refer to 3 different layers that comprise the Fedora base image that we are downloading.

note: fedora:latest

Remember we are downloading this image from the public Docker registry. (Docker Hub) On Docker hub there just happen to be a bunch of different version of Fedora. If we do a Docker run command for fedora (or any other image), Docker will grab the one that is tagged as the latest version for that image.

*[Command:]{.underline}*

docker pull

We use the Docker Pull command, to pull images from Docker hub and install them locally. So we don\'t have to wait around for them to download when we are firing containers up. For now we can do a simple:

\- docker pull fedora

But this would only download the image tagged as the \*latest\* but if we add \'-a\' behind fedora we will get them all

\- docker pull -a fedora

Now, let\'s try 

\- docker images fedora

We will get the list of images we have downloaded with the name fedora. Since we downloaded \*all\* of them, the list contains various elements. The one thing to not is that some of the image ids repeat. The reason for that is that we can see which version is which by looking at the tag which shows both, the version number and the official name for that release. There are some that are by themselves...for example: rawhide is by itself so we can consider them to be the non-stable release of fedora.

So, in general, images are static of frozen version of containers. They contain all of the data and metadata to fire up a container. We can view locally store images with the "docker images" command and we can pull images from the docker hub with the "docker hub\"

When these images are downloading, we can see that we **lunch containers from images**.

**Once downloaded, images are stored in the host file system under:**

**/var/lib/docker/**

**Containers**

Alright, so Containers are lunch from images. We can think of them as running instances of an image.

We can think of images as our Build-time construct, and containers as our Run-time construct.

We use

\- docker run

To launch a container. We know that docker goes ahead and grabs the image that we specify, unpacks it, stacks all of the layers and builds it in into a runner container.

\- docker run -it ubuntu /bin/bash

-   After docker run we add any flag that we want

    -   -i Makes it an interactive container

    -   -t To assign it a sudo tty

-   Then we specify the image we wanna lunch it from.

    -   ubuntu

-   Then we tell it which process or application to run

    -   /bin/bash (so far we have done this one....but it\'s not the only option. /bin/bash Will just allow us to log in and get a terminal

**A container is effectively a RUNNING linux instance. (Bare bone Linux machine).....** We have said this in the past....but in what ways is it a bare bone Linux machine?

Well, for example, the fedora images we pulled down, they are about \~250 MB. That\'s pretty small for a modern OS, so there is clearly a bunch of stuff not in there we normally get if we perform even  minimal install of fedora.

In general, container optimized OS images tend to have the bare minimal packages installed. No GUI or anything. 

Let\'s try going back to the fedora container from before...

// On the tutorial they already had it running. But mine was off. in order to start it we only need to type:

\- docker start

// Make sure you have sudo rights

And then, in order to access that container, we attach to it\...

\- docker attach

If we now try things like:

\- pstree

// Command not found

\- man

// Command not found

\- iostat

// Command not found

So this containers really are minimal. Just the thing needed to provide a functional run-time

**// We can exit a container without killing it by:**

**---\> Ctrl + P + Q \<--- **

Remember unless we specify the name of the container we are dealing with, we will automatically get assigned a random name to us.

**Registries and Repositories**

We pull images from Repos or Repositories and Repositories live inside of Registries. For example, the public registry for Docker is "Docker HUB". So within Docker Hub we have lots of Repos. The one\'s found here are generally trusted and maintained by Docker Inc and (....Kenotecle?) and between the two of them they sort of ensure that we are getting the official releases.

Within each repo, we then have the images. So, let\'s think of Ubuntu, the images would be 14.04, 12.04, all of that.

*[User Repos:]{.underline}* User Repositories are repos containing images created by members of the Docker community.

Always be extra careful before downloading random containers in our environment. Make sure to trust the source of the containers we want to use.

**Module Recap**

![](001_02_-_Docker_Deep_Dive_-_Major_Docker_Components_002.png)
