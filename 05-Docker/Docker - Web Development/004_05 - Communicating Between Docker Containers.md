05 - Communicating Between Docker Containers

Friday, April 29, 2016

12:12 PM

 

Docker provides 2 different technologies we can use to link up our contianers:

 

1.  Use Legacy Linking (using names)

    a.  Easy to use and setup

2.  Add Containers to a Bridge Network

    a.  Newer option

    b.  Create isolated network that only a set of specified containers can use

 

 

**Linking Containers by Name (Legacy linking)**

 

Steps to do legacy linking:

1.  Run a Container with a Name

    a.  docker run -d **\--name \<name\>** postgres

        i.  docker run -d my-postgres postgres

2.  Link to Running Container by Name

    a.  docker run -d -p 5000:5000 **\--link \<name\>:\<container alials\>** ikanant/node

        i.  docker run -d -p 5000:5000 \--link my-postgres:postgres ikanant/node

3.  Repeate for Additional Containers

    a.  ![Machine generated alternative text: 3 Repeat for Additional Containers Run a Container Repeat with a name Link to Named Container ](004_05_-_Communicating_Between_Docker_Containers_000.png){width="5.0in" height="3.525in"}

 

 

**Container Networks (Bridge Networks)**

 

The idea is simple: As developers we can create a private Docker Isolated Network that will allow the containers in it talk to one another without giving out their content to any other containers outside of such network.

 

![Machine generated alternative text: Isolated Network 1 o Docker Host Isolated Network 2 ](004_05_-_Communicating_Between_Docker_Containers_001.png){width="5.0in" height="3.533333333333333in"}

 

Steps to Create a Container Network

1.  Create a Custom Bridge Network

    a.  docker **network create \--driver bridge \<network name\>**

        i.  ![Machine generated alternative text: Name of custom network - -driver bridge isolated_network docker network create Create a custom use a bridge network network ](004_05_-_Communicating_Between_Docker_Containers_002.png){width="5.0in" height="2.1416666666666666in"}

2.  Run Containers in the Network

    a.  docker run -d **\--net=isolated_network** \--name mongodb mongo

        i.  ![Machine generated alternative text: docker run \"Link\" to this container by name -d ----net=isolated network \--name mongodb mongo Run container in network ](004_05_-_Communicating_Between_Docker_Containers_003.png){width="5.0in" height="2.5in"}

 

-   docker network ls

    -   Will show networks

 

Do we really need to type SO MANY commands to link containers....the answer is NO: Here comes Docker Compose

 

![Machine generated alternative text: docker ](004_05_-_Communicating_Between_Docker_Containers_004.png){width="2.6666666666666665in" height="3.7583333333333333in"}
