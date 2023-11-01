03 - Hooking Your Source Code into a Container

Friday, April 29, 2016

12:11 PM

**The Layered File System**

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_000.png)

In Docker we can think go the layered file system as: Layers of files that build on top of each other.... Which is good for many things, for example: disk space and re-use...

Lets consider we download the Ubuntu Image from Docker Hub....This image comes down with a series of layers we see get downloaded. Image layers get stacked on top of one another and once an image is set in place and another gets added on top, then the underlying image(s) is READ only....

This can seem problematic to some people interested to use such images for database hosting etc.... But that's where Containers come into place. In a way we can think of containers as Images that have a separate layer on top that actually allows Read/Write tools to the user.

**Containers CAN Share Image Layers**

This comes into place with what I mentioned before regarding Re-usability of layers. If I were to use this Ubuntu Image for a list of containers, then all these images would jus t get reused.

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_001.png)

**How do you get source code into a container?**

At a minimum we can always put it in the Image itself ( we will cover this in the future ) ... Well, for this we will need to learn about Volumes

**Containers and Volumes**

***Docker Volumes:***

-   Special type of directory in a container typically referred to as a \"data volume\"

    -   Typically called DATA volumes because we can technically store in them ANY kind of data

-   Can be shared and reused among containers

-   Updates to an image won\'t affect a data volume

-   Data volumes are persisted even after the container is deleted

The way we can think about Volumes is as separate folders stored in the Docker Host machine (in our case our Linux virtual machined named \'default\') These volumes are nothing more than a folder stored in the machine that can be read from or written too by our containers... in any case that a container gets deleted, this doesn\'t force the volume to get deleted with it. It will just stick around our Linux Host machine until we want it too.

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_002.png)

For our example we are actually going to drop our source code for our application inside a Volume

**My Take:** When wanting a container to have access to a Volume to write too, Docker will be smart enough to create such container inside a default /mnt/.../.../.../\_data folder which will then attach our personal directory to that default path: /src/www/...

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_003.png)

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_004.png)

This can be seen as a way to organize our data inside volumes but that can also be somewhat confusing with such long paths... as developers we can change the root folder for which our containers get their data from. The custom folder that we can set up to use as our volume can be in our Host Machine like usual, OR we can also have it in our local ACTUAL Windows or Mac machine.

NOTE: pwd = current working directory

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_005.png)

So what this will do is create a VOLUME in the container which is going to be var/www

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_006.png)

![](002_03_-_Hooking_Your_Source_Code_into_a_Container_007.png)

**My take:** Docker run will just spin out a container

-   -p 8080:3000 Will match the Host Machine (default) port to be 8080 to the containers port 3000

-   -w Will setup our work directory (where our source code is at)

-   Node Is the name of the image we are spinning a contianer from

-   Npm start Is the script we are running inside that src folder

**Removing Volumes**

docker rm -v \[container name\]
