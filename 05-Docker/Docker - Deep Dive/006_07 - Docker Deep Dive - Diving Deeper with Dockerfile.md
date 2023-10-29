07 - Docker Deep Dive - Diving Deeper with Dockerfile

Friday, April 29, 2016

11:45 AM

 

Course taught by: *Nigel Poulton*

**The Build Cache**

In this DEMO we will go into the Pluralsight folder we created before in which we have the Dockerfile we used in the previous tutorial

\- docker build -t="build1" .

-   -t: We will tag it: "build1\"

Here it will do a bunch of work. It will take a while. At least a minute. Now, let\'s build the same command again but this time let\'s tag it with "build2\"

\- docker build -t="build2\"

-   this was FAST. why???

Well, the reason why this happened SO FAST is because of the [build cache]{.underline}. Basically, when we  build a new image, the Docker Daemon iterates through our Docker file executing each instruction, as each instruction is executed the daemon checks whether or not it\'s got an image for that instruction already in its build cache.

*[Build Cache:]{.underline}* When we build a new image:

1.  The Docker Daemon iterates through our Docker file executing each Instruction

2.  As each instruction gets executed the daemon checks if wether or not it got an Image with that instruction already in it\'s build cache. If it does it will save time for us.

3.  What the Daemon basically does is to look at our base image and it looks at ALL child images that it got linked or associated with that Base Image. and It checks if any of them has been built with the same instruction that is about to execute

4.  If it does, GREAT, it just uses the Image from the cache, and creates a new LINK

5.  If there ISN\'T, then is off to the Build run to do some work to Build it.

**Dockerfile and Layers**

Starting once again from a clean system with a simple ubuntu:15.04 system. If we do a:

\- docker info

// We see that we have 4 images total.....which we know are the amount of layer the ubuntu image contains...now, let\'s use the Dockerfile that we created before, it looks something like:

/\*

#Ubuntu based Hello World container

FROM ubuntu:15.04

MAINTAINER <jonathan.hdez92@gmail.om>

RUN apt-get update

RUN apt-get install -y apache2

RUN apt-get install -y vim

RUN apt-get install -y golang

CMD \["echo", "Hello World"\]

\*/

So, how many image layers do you think this will add to our already existing 4 images?

Answer: 6

This time there was no build cache so it took a while to get everything ready for the build.

Why did it add 6 layers?

\- docker history

// This will list events in reverse order.

So 6 Dockerfile instructions created 6 layers. We can do things to reduce the amount of layers that Dockerfiles creates when building new images, but for now the main knowledge to take is:

*[MOST instructions that we shoot in a  Dockerfile results in a new Image layer that is created]{.underline}*

**Building a Web Server Dockerfile (MORE DOCKER FILE INSTRUCTIONS - VOCABULARY TIME)**

We will build a Web Server to run as a container. We will build it from a Docker file, launch it as a container and test it. Then we will come back to our Dockerfile, add some more instructions, build it again, and test it again....then again.....then again.... Adding and learning instructions as we go.

Create web folder, and create a Dockerfile using VIM\...

/\*

#Simple web server for Pluralsight course

FROM ubuntu:15.04

MAINTAINER <jonathan.hdez92@gmail.om>

RUN apt-get update

-   Let\'s make sure our image starts up its life with the right foot with an up to date copy of package list from source

RUN apt-get install -y apache2

RUN apt-get install -y apache2-utils

RUN apt-get install -y vim

-   We are getting a bit convoluted here, but please remember that this examples are necessary somewhat convoluted so we can test some stuff. In the real world, sure we wouldn\'t include the apache util package or the VIM package on a web server I plan to run inside of a container...but this is a classroom and we are going to use this to illustrate image layers.

RUN apt-get clean

-   To get rid of any any debt packages in our local apt cache

-   We are not going to try to re-install any packages or anything like that. If this image doesn\'t work we are just throw it away and create another one.

-   In order to keep containers lean and clean I always clean up the apt cache

-   **YES, this apt-get clean won\'t help the way we are writing our docker file at the moment. We will cycle back and explain why a little later**

EXPOSE 80

-   We will export port 80 from our container. This EXPOSE will make sure that port 80 in ANY container that is pinned up from this image is available to the Dockerhost is running on. This is the first bit of container networking

CMD \["apache2ctl", "-D", "FOREGROUND\"\]

-   We will go more in depth why we write command in the EXEC style a little later in the course.

-   Take it as it is, this will start our apache web server

\*/

\- docker build -t="webserver" .

// This will build our image

**Launching the Web Server Container**

\- docker run -d -p 80:80 webserver

-   -d: Detached. It means we are not gonna go into the shell of this container

-   -p 80:80: Map port 80 on our host to 80 in our container

Now from here we can test the container running from our BROWSER, but we have to configure the DNS name for our VM so, I couldn\'t get around to check that. Note that if we try to do a docker ps, our web server container will show up until we manually stop it.

**Reducing the Number of Layers in an Image**

We can see that every one of our apt-get RUN instructions has created an additional layer. So, let\'s fix that\...

One thing that we can do is just write:

RUN apt-get update && apt-get install -y apache2 && \...

And this would work BUT, it is not pretty. It would look a lot prettier and a lot cleaner if we make the effort to spread it within a few lines.

example:

/\*

#Ubuntu based Hello World container

FROM ubuntu:15.04

MAINTAINER <jonathan.hdez92@gmail.om>

RUN apt-get update && apt-get install -y \\

     apache2 \\

     apache2-utils \\

     vim \\

     && apt-get clean \\ 

     && rm -rf /var/lib/apt/lists/\* /tmp/\* /var/tmp/\*

EXPOSE 80

CMD \["apache2ctl", "-D", "FOREGROUD\"\]

\*/

From here we will save time AND space. The docker file we create will be smaller in size.

**The CMD Instruction**

This guy is kind of similar to RUN, in that it executes commands, but it is very different too. CMD *[ONLY]{.underline}* executes at run time. So when we execute a container. RUN on the other hand is a build time instruction. We more often than not we use RUN commands to add layers to images and install app to images. CMD runs a command inside of our container when it\'s launched. It\'s equivalent to the command that we attach to the end of the Docker RUN command. Do note though, that if we write any command to the end of the DOCKER RUN command, this will overwrite whatever we have written on the Dockerfile under CMD. **There can only be ONE cmd instruction per Dockerfile.** We could write more than one, but only the last one will be effective. 

 

 

<table>
<colgroup>
<col style="width: 64%" />
<col style="width: 35%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>CMD</strong></th>
<th><strong>RUN</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul class="incremental">
<li><p>Run-time</p></li>
<li><p>Run Commands in containers at launch time</p></li>
<li><p>Equivalent of:</p>
<ul class="incremental">
<li><p>docker run</p></li>
<li><p>docker run /bin/bash</p></li>
</ul></li>
<li><p>One per Dockerfile</p></li>
</ul></td>
<td><ul class="incremental">
<li><p>Buil-time</p></li>
<li><p>Add layers to images</p></li>
<li><p>Used to install apps</p></li>
</ul></td>
</tr>
</tbody>
</table>

*[Style of Syntax:]{.underline}*

The CMD takes to styles of input:

1.  Shell Form

    -   Takes the commands, arguments, variables and treats them in exactly the same way they\'d be treated by the shell itself.

    -   Behind the scenes, if we specify arguments to the running instructions in shell form, they get automatically pre-pended with "/bin/sh -c\"

    -   Example 1: CMD echo "Hello world\"

        -   And we would end up with containers that would print Hello world every time they started. And they would exit because remember that containers exit as soon as the process they are running exits.

    -   Example 2: CMD echo \$var1

        -   Variables get expanded just as they do with the shell. 

2.  Exec Form

    -   We pass arguments to CMD formatted like a JSON array. A comma separated list of values, each values enclosed in double quotes, and everything enclosed in closed brackets

    -   Recommended method.

        -   It allows commands to be executed inside of containers that don\'t have a shell.

        -   It avoids any potential String munching by the shell.

    -   BAD

        -   We don\'t get any of the goodness of the shell

            -   No variable expansion

            -   No special characters (&&, \|\|, \>... .)

**The ENTRYPOINT Instruction**

Well, even though we just said a CMD command can be used to run a command inside of a container and there is nothing wrong by doing that. (We have even use it in our demos. BUT the better, and prefer method of specifying the default act to run inside of a container is by the ENTRYPOINT instruction.

Why?

-   Entry point can\'t be overridden at run-time with normal commands - docker run ...

    -   This can be a good or a bad thing though

    -   The COOLNESS: Anything we do specify at the end of the run command at run time get\'s interpreted as arguments of the ENTRYPOINT instruction

    -   Example: ENTRYPOINT \["echo"\]

        -   Any container we spin off of images that have this command are going to run the echo command.

        -   Now, if we spin this container: - docker build =t="hw2" .

        -   When running the container off of it: docker run hw2 Helloooo there!

            -   We see: Hellooooo there! as in an echo was called.

        -   Let\'s try: - docker run -it hw2 /bin/bash

            -   Here we want to get an interactive container and get in the shell using /bin/bash

            -   Result: we just echoed: /bin/bash..... NO shell for us 😃

-   Let\'s say we have some CMD command in our Dockerfile?

    -   Well, those CMD command will be treated similarly as arguments for the ENTRYPOINT command, as long as they have been written in Exec form. But REMEMBER, if we do type anything after the run command to spin up a container, then the CMD commands will be overwritten.

    -   This is GREAT, because it will pretty much let us have default Arguments for our ENTRYPOINT. And have the ability to override them at run time.

**The ENV Instruction**

Passing Environment variables to continuers....We do that with the ENV instruction

ENV var=value

name of the variable = value to store int he variable.

These variables are then available inside of the running containers as normal Environment variables

Example 1:

ENV var1=Nigel var2=Poulton

Let\'s build and spin a container form it.

\$env

We will see the variables listed.

Cool example:

ENV var1=ping var2=8.8.8.8

CMD \$var1 \$var2

When we spin the container and do a docker ps we see the container running.

\- docker logs

And we will see the result

\- docker logs -f

We will see the pings as they happen live

**Volumes and the VOLUME instruction**

Volumes are under development by Docker. A guess: At a bare minimum we will see a dedicated *[docker volume]{.underline}* subcommand that will allow us to manage Volumes.

Volumes are all about decoupling data volumes from Containers. And they are also about SHARING data between containers. Basically a way to store the data in a directory on the Docker HOST file system. These way, if the container get\'s stopped or even deleted the DATA persists. As it\'s decoupled from the container.

\- docker run -it -v /test-vol /test-vol ---name="voltainer\" ubuntu:15.04 /bin/bash

-   Specify a volume like: -v  

-   ---name=

Once we run this we will get inside of our container. And then

\- ls -l

We ca the see "test-vol" folder in there

Docker created that Volume when it created the container. If the directory DOES exist, then normal UNIX mount rules apply: Any data that already exists in the mount vol becomes UNAVAILABLE while there is a Volume mounted in it

If we exit the container and do a quick - docker inspect We can see the Volumes we have and it\'s data. We can go to the file and see how it\'s listed as ReadWrite

Now let\'s say we spin up a new Container:

\- docker run -it ---volumes-from=voltainer ubuntu:15.40 /bin/bash

And then

\- ls -l

There it is! We can access that folder and it\'s data from this container even if the ORIGINAL container is stopped or deleted

To delete VOLUMES the only current way is to type from it\'s container:

docker rm -v

![](006_07_-_Docker_Deep_Dive_-_Diving_Deeper_with_Dockerfile_000.png)
