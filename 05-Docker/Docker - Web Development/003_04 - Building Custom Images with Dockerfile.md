04 - Building Custom Images with Dockerfile

Friday, April 29, 2016

12:11 PM

 

**What is a Dockerfile?**

A docker file is nothing more than a text file with instructions in it. These instructions are made specifically for Docker.

 

**My Take:** In the developer world, whenever we write code for JAVA or C++, we run that code through a compiler whose job is to convert that to machine code and run it on our computer.

 

In the Docker world we take this Dockerfile and we run it through our client. Which will generate a Docker image

 

**Dockerfile Overview**

-   Text file used to biold Docker Images

-   Contains build instructions

-   Instructions create intermediate image that can be cached to speed up future builds

-   Used with \"docker build\" command

 

**Commands:**

-   FROM

    -   NodeJS Image, MongoDB, Ubuntu, etc

-   MAINTAINER

    -   Our name

-   RUN

    -   We can have different things defined that will be ran inside our container

    -   Example: npm install

-   COPY

    -   Copy instruction can be used to copy source code into our container to be deployed to production

-   ENTRYPOINT

    -   Can be a JAVA, NODE or PYTHON command to start the code

-   WORKDIR

    -   Sets the contexts to where that container is going to run.

    -   What folder has my project.json to run for example

-   EXPOSE

    -   This would be the default PORT that the container will run internally with

-   ENV

    -   Define environment variables

-   VOLUME

    -   Define volumnes

 

**Example:**

 

 

![](003_04_-_Building_Custom_Images_with_Dockerfile_000.png){width="5.0in" height="3.7in"}

 

 

**Building our Custom Image**

 

![Machine generated alternative text: Building a Custom Image docker build Tag name -t cyour username\>/node Short for \--tag Build context ](003_04_-_Building_Custom_Images_with_Dockerfile_001.png){width="5.0in" height="3.066666666666667in"}

 

Keep in mind that by default, when running a docker build command, Docker will automatically look for a file named \"Dockerfile\" but in the case we name it something different, then we can use a f flag.

 

Example: docker build -f mydockerfile.txt

 

[docker build -f Dockerfile -t ikanant/node .]{.mark}

 

&&

 

[docker run -d -p 8080:3000 ikanant/node]{.mark}

 

 

**Pushing an Image to Docker Hub**

 

Docker push \<your username\>/node

 

![Machine generated alternative text: Summary Dockerfile is a simple text file with instructions that is used to create an image Each Dockerfile starts with a FROM instruction Custom images are built using: docker build -t \<username\>/imageName Images can be pushed to Docker Hub ](003_04_-_Building_Custom_Images_with_Dockerfile_002.png){width="5.0in" height="2.2416666666666667in"}
