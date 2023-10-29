05 - Docker Deep Dive - Building from a Dockerfile

Friday, April 29, 2016

11:44 AM

 

Course taught by: *Nigel Poulton*

**Introducing the Dockerfile**

**Capital sensitive name: Dockerfile**

It\'s a regular old TEXT file. Yes, with it\'s syntax, but it\'s a human readable plan text file. It is comprised of INSTRUCTIONS that define HOW to build an Image. These instructions get read, one at a time starting from the Top down the Bottom, Left to Right.

Although it can live anywhere in our system! we have to choose very carefully where we want it to live.

*[When we start to build an image out of a Dockerfile, ANY files and directories within the same location of the Dockerfile or further down in the directory tree get\'s included in our build.]{.underline}* So we definitely don\'t want to put our Dockerfile in ROOT for example.

Run **docker build** command to build an image from a Dockerfile

**Creating a Dockerfile**

Dockefile Rules:

-   The FROM instruction has to be the first instruction in the Docker file

-   Standard practice to capitalize instructions

-   All of the lines follow the format: \[ INSTRUCTION value \]

#: Any line that starts with a \# it\'s a comment.

ex: #Ubuntu based Hello World container

*[Instructions]{.underline}*

-   FROM

    -   It tell us which Image we are going to base this image on

    -   ex: ubuntu:15.04

-   MAINTAINER

    -   Here we will write our email address

    -   Can be written anywhere but should be at the top for good practice

-   RUN

    -   ex: apt-get update

    -   We use RUN instructions to run command against our images

        -   Often to install Software Packages: like nginX or golang

    -   *[Every RUN instruction creates a new layer in our image]{.underline}*

        -   The way it actually works is that, let\'s consider we have 3 different RUN commands....well, Docker first get\'s to the first RUN, it creates a Container based on our base Image and runs the command we specified (Creating one layer).... then it commits this changes to a new Image layer. The next RUN command then launches a NEW container from the new Image layer we just committed, executes its command, Stops the container again and then commits it\'s new layer.....

            -   10 RUN commands means, 10 layers

            -   This is not the end of the world but it is not ideal either. We will avoid this later in the course

-   CMD

    -   Short of Command

    -   ex: CMD \["echo", "Hello World"\]

**Building an Image from a Dockerfile**

\- docker build -t helloworld:0.1 .

-   t: To apply any tags to our image (Isn\'t mandatory but it is HIGHLY recommended)

-   . : This directory

-   This will build a NEW docker Image named helloworld

Notice the last line: Successfully built

Notice: Sending build context to Docker daemon 2.048kb

Well, build context is the files and directories in the directory where our Dockerfile was. In this case it was only our Dockerfile itself so, small 2.048kb.

It is CLEARLY the docker daemon and not the client that does the build. In our example we are running the client and daemon on the same machine but remember earlier we talked about configuring a docker client to talk to a remote docker daemon over the network. In those type of situation we need to be careful with the potential impact of sending lots of data over the network.

Then we can see the daemon stepping over the different actions in our Dockerfile:

1.  Step 0: FROM ubuntu:15.04

2.  Step 1: MAINTER

    1.  This will spin up a container, adds the new image layer and then REMOVES the container

3.  Step 2: apt-get update

    1.  Spins up a new continuer. We see the the output of the apt-get update and once that is done, a new image layer get\'s committed and the container it used get\'s thrown away. [It is the container that get\'s thrown away, NOT the images. We keep those.]{.underline}

4.  Step 3: echo "Hello world\"

    1.  Spin up a new container, commit a new image, then throw away the container.

5.  Then boom, image created

Now, in order to run a container up from our new image we just do:

docker run And there is our hello world container.

Note that with RUN command we can add commands with the && sign. That way we don\'t have create image layers for EVERY SINGLE echo command for example.

 

![](004_05_-_Docker_Deep_Dive_-_Building_from_a_Dockerfile_000.png){width="5.0in" height="2.775in"}
