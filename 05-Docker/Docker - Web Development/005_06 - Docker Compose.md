06 - Docker Compose

Friday, April 29, 2016

12:12 PM

Great way to get multiple containers to be up and running with a minimal effort of our part

![Machine generated alternative text: docker ](005_06_-_Docker_Compose_000.png)

**What is Docker Compose?**

Is a great way to automatically manage the lifecycle of our application in the development environment to get it up and running and stop it very very quickly.

**What does it do?**

It allows us to handle multiple images and turn those images into containers. This is similar to what we are commonly used too by typing docker run and so on....but in this case, Docker Compose will make ouyr life much easier and less repetitive and promt for errors.

**Docker Compose Features:**

1.  Manages the whole application lifecycle:

    a.  Start, stop and rebuild **services**

        i.  And services are pretty much RUNNING CONTAINERS. We are just going to call them services in the world of docker compose

    b.  View the status of running services

    c.  Stream the log outpot fo runnning services

    d.  Run a one-off command on a service

**Whats the need of Docker Compose?**

![Machine generated alternative text: The Need for Docker Compose NGMX nodeo redis nodeo nodeo mongoDB Docker Compose (docker-compose.yml) ](005_06_-_Docker_Compose_001.png)

>  

In this case we are dealing with 6 different Docker Containers and we are going to manage them all through our docker-compose.yml file.

The **docker-compose.yml** is written in a very easy format

![Machine generated alternative text: Docker Compose Workflow Build Services Start Up Services Tear Down Services ](005_06_-_Docker_Compose_002.png)

**The docker-compose.yml File**

-   This fille will define ALL of our services

-   We can run it through docker-compose BUILD process...which, similarly to what we have seen before will generate docker images from our Dockerfiles.

![Machine generated alternative text: The Role of the Docker Compose File o Docker Compose Build docker-compose.yml (service configuration) Docker Images (services) ](005_06_-_Docker_Compose_003.png)

**What do we include in this Dockerfile?**

![Machine generated alternative text: Docker Compose and Services version: \'2\' services: nedeo mongo DB docker-compose.yml ](005_06_-_Docker_Compose_004.png)

**Configuration Options that we can Supply to our docker-compose.yml:**

-   Build

    -   What folder do we build from and what Dockerfile

-   Environment

    -   We can define Environment variables. Can be automatically set these variables inside the created containers at Run time

-   Image

    -   Sometimes we already have an image ready to go in our local machine or in the cloud and we just want to use that for our service

-   Network

    -   Way to link up services (similar to the bridge network we talked before)

-   Ports

-   Volumes

![Machine generated alternative text: docker-compose.yml version: \'2\' services: node: build: context: . Example dockerfile: node.dockerfile networks: -nodeapp-network mongodb: image: mongo networks: - nodeapp-network networks: nodeapp-network driver: bridge ](005_06_-_Docker_Compose_005.png)

**Docker-compose Commands:**

-   docker-compuse build

    -   Similar to what we have already done in the past

>  

-   docker-compose up

    -   Start the defined services up as running containers

-   docker-compose down

-   docker-compose logs

-   docker-compose ps

    -   List different containers that are running as our services

-   docker-compose stop

    -   Stop all different services

-   docker-compose start

-   docker-compose rm

    -   Remove the different contianers that are making up our services

**Building Services**

![](005_06_-_Docker_Compose_006.png)

Or we can build an individual Service:

![](005_06_-_Docker_Compose_007.png)

**Service Start:**

![](005_06_-_Docker_Compose_008.png)

![](005_06_-_Docker_Compose_009.png)

Teare Down Services

![](005_06_-_Docker_Compose_010.png)

![](005_06_-_Docker_Compose_011.png)

**Docker-compose.yml Example:**

![](005_06_-_Docker_Compose_012.png)
