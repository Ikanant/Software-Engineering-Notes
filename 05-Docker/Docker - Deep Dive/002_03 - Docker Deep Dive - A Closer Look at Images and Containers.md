03 - Docker Deep Dive - A Closer Look at Images and Containers

Friday, April 29, 2016

11:43 AM

 

Course taught by: *Nigel Poulton*

**Image Layers**

Remember: Images are like static, frozen in time Containers and are what we launch containers from.

We talked about how they are layered or stacked. Time to see what that is all about\...

In Docker terminology, most times we refer to these layers as: IMAGES. We can consider an Image that is made by three layers. In a way, we have 3 images that create a single image. These would work pretty much like this:

-   Layer 0: At the bottom we have our Base Image (Root). This is where we have our Root file system (ROOTFS). All the files and directories required to make our container stripped down bare minimum OS. If it\'s an Ubuntu based container, that are all the files need to make our container look and feel like an Ubuntu OS.

Now, let\'s say we install an application...something like NGinX

-   Layer 1: nginx

-   Layer 3: Patches or Updates for our content files.

So, why do we need 3 images? Why can\'t we just have one image with everything inside of it? Well, we are trying to step away from the monolithic structure of applications where if we want to change or add anything we need to crack open our already defined structure. By having three different layers within an image (and possibly more) we can just go ahead and add or remove layers for the things that we want out of our image. Easy plug and play environments. Which makes it extremely helpful when basing multiple containers off the same image root.

***Union Mounts***

Each layer, or image, gets it\'s own unique id...and then these IDs are listed inside a Docker image and some of the metadata that tells Docker how to build a container at runtime. So our metadata from the above example would tell Docker to put Image ID abc(Ubuntu OS) at the bottom as the parent or the base image then place def(NGINX) and then chi on top of that. Then these get confined into a single combined view of all layers. With the data in the higher levels hiding the data in the lower layers.

If there is a conflict...Let\'s say we have xzresult.conf in the base image but an updated version of it in the top layer, well the top layer wins. The higher level ALWAYS win when there is a conflict. And this is all pull together under the hood by the magic of Union Mounts.

Union Mounts let us mount multiple file systems on top of each other. So with Union Mount, instead of mounting one file system, let\'s say ROOT, and another /HOME. Well Union Mount let us stack multiple file systems over the top of each other. But they convine all of the layers into a single view. Giving us, or the application or the operating system, the look nd feel of a single regular everyday file system.

The way the Docker runs with all these Union Mounts, is that all of these layers in the image are mounted as READ ONLY. and then the top layer, which get\'s added only when we launch the container, is the only WRITABLE layer. So, with Docker, it\'s only ever the very top layer to be WRITABLE.

Now remember, the base image at the bottom has our ROOTFS, well it is important to know that there is actually another layer bellow that. SOMETIMES.

When we start a container there is actually a small BOOTFS that exists bellow our ROOTFS. The BOOTFS is very short lived, it\'s not there after the container started.(we never have to deal with it though). It\'s really light weight. The process of starting container isn\'t quite the same as booting a full blown Linux VM.

*AUFS is the default Union Mount implementation used on Ubuntu Hosts running Docker.*

**Where Images are Stored**

\- docker pull cores/apache

/\* Notice that multiple layers get downloaded. Each of these is a layer that form the CORE OS apache Image. I can\'t note on this class because ---tree option was deprecated.\*/

**Copying Images to Other Hosts**

Let\'s see how we can move a Docker Container, from one Docker Host to another. Later in the course we will learn how to do this by pushing our containers to the Docker Hub and then downloading them from Docker Hub on another host. But right now we will do it the manual way.

We will manually save a container Image to a TAR file, export it from our Ubuntu Docker Host and Import it on our CentOS docker HOST.

\- docker run ubuntu /bin/bash -c "echo \'cool content\' \> /tmp/cool-file\"

-   Remember we got the Ubuntu image locally and if we do not specify a version we are going to get the one tagged as \*LATEST\*

-   We will tell bash ---\> to run \*echo" and to create a file called cool-file with \'cool content\' as it\'s single line content

-   This time we DO NOT have -i or the -t. Why?

    -   The command that we are running inside of the container is a short lived command. Basically it will run and as soon as it\'s complete, the container will exit. So, no point on interacting with the shell

    -   The most common way to run containers is in the "Detached" mode. Where we are not running -i or -t on it.

What we just did is that we started a container, and created a new file with a single file of content inside of it. Similar to this, we could have just as easily installed an app. Patch the image to the container or added new config files. The important thing is: WE MADE A CHANGE

\- docker ps -a

// -a: Will show us all container that have run in the past but aren\'t necessarily running now.

\- docker commit

-   What this has done is to create a NEW image from the changes that we just made inside of our container. 

-   *[Docker commit takes the changes that we make and creates a new IMAGE.]{.underline}*

\- docker images

// This will show the image that we just created. Which automatically will bet tagged with latest and the name we specify.

\- docker history

// COOL, we can even see the command that we use when creating this image. So, for us a quick shell command and a difference of 13 bytes! So, our new image, and any container that we base off of it, will share a common Ubuntu base image as READ ONLY, and have our common 13 byte layer also as READ ONLY. Then of course they get their own writable own layer. The point being though we could have 10 , 20 or 100 containers running on this, all sharing the same Ubuntu based and Thin layer. UBER space efficient.

\- docker save -o /tmp/.tar

-   -o: Output to

-   first file path is where the outfield will go and it\'s name

-   second file is the name of the image we are exporting

Now we will go to our CentOS machine and copy the created TAR file over there. We named our TAR file "fridge\"

\- docker load -i

-   i: Import

Open it:

\- docker run -it fridge /bin/bash

// Boom, we are inside the container we created within our Ubuntu machine.

**The Top Writable Layer of Containers**

Images are used to launch containers. So Containers are run-time instances of Images.

When we launch containers with "docker run" command, the docker engine reads the image and any metadata and builds the container by stacking the different image layers and stacks them, as per the instructions found in the Image metadata. And then... **Each and every container get\'s it\'s own [Thin Writable]{.underline} layer that slaps on top of the READ only image layers below it.** It is here, in this top layer, where all the changes to the containers are made. (Installing and updating applications, writing new files, config changes like IP address) it all goes there. This top layer is where all the container state is stored. These top layer is INITIALLY empty, and then it only consumes space as and when we make changes in our container.

An interesting thing: **The ROOTFS of a CONTAINER, is actually never made WRITABLE.**

![](002_03_-_Docker_Deep_Dive_-_A_Closer_Look_at_Images_and_Containers_000.png)

**One Process per Container (usually)**

Generally speaking, Containers run a single app or a single process. When the process running inside of a container EXITS so does the Container. Recall when we ran the container and only create a file inside.

\- docker run -d ubuntu /bin/bash -c "ping 8.8.8.8 -c 30\"

-   -d: Detached, or in the Background

-   -c: Command?

For this example, when we type "docker ps" We will see the container still running.... if we type "docker top then we can see the last thing (so far) that the process is doing. After a while, if we type:

\- docker ps

// Nothing. The container we just created EXITED. **Container exist while the processes running inside of them exist.**

[Recall]{.underline}**:** So far we have not specified the version of the image we are using to create our container. In order to be careful with that we will type

Command:

\- docker run ubuntu:14.04

// Or something like this. We should always be explicit so we know exactly what we are getting.

**Commands for Working with Containers**

The Docker RUN command is a bit of a UBER command. It already has a major list of switches and options attached to it. So far we have seen -i and -t and we have used those when we want an interactive container with a shell. Then how about -d To run a container detached in the background

Other Options:

-   ---cpu-shares=256

    -   To Control how many CPU shares the container gets. With this option 1024 it would be full access to all CPUs so, 256 would be a quarter

-   memory=1g

    -   This would give our container 1 gig worth of Host memory to our container

-   etc\...

Reference page:

docs.docker.com/engine/refence/run/

\- docker inspect

-   We will get detailed information on the container. We can also run it against Image ID too.

\- docker attach

To exit, we can press CTRL + C

Let\'s say that we have a container doing a process like pinging 8.8.8.8. If we press CTRL+C we would cancel....the process AND the container itself.

![](002_03_-_Docker_Deep_Dive_-_A_Closer_Look_at_Images_and_Containers_001.png)
