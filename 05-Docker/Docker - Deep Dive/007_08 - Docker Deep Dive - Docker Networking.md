08 - Docker Deep Dive - Docker Networking

Friday, April 29, 2016

11:45 AM

 

Course taught by: *Nigel Poulton*

**The docker0 Bridge**

We are on our Local Host with the Docker daemon running and NO container started.... let\'s take a look at the network stack:

\- ip a

Here, ignore lo, or eth0 or eth1, they got nothing specific about them. BUT, take a look at the bottom...we can see docker0

When the Docker Daemon starts in our Docker Hosts, it creates a docker0 interface....*[But it is a bit more than just an Interface]{.underline}*... It\'s actually a BRIDGE, or a virtual switch created entirely in software inside the Linux Kernel. **docker0 is crucial to Container Networking**. 

As a bridge or a virtual switch: Just as we might consider a normal physical switch, it passes or switches packets between two connected devices. So, this is an internet switch, just one that is implemented entirely inside the Linux kernel. But, NORMAL switches got ports and devices attached to them, well if this is 100% software, how can we see what is connected to it?

If we got the bridge-utils pack installed in our system, we can check\...

apt-get install bridge-utils

yum install bridge-utils

With that we can check the details of docker0 with:

\- brctl show docker0

From here we can see

-   Bridges name

-   Bridge ID

-   STP: If it has spanning tree available

-   List of connected interfaces

We don\'t see ANY interfaces now because we got not containers running. And as we launch containers we will see them pop up on the output of this command.

**Virtual Ethernet Interfaces**

We\'ve got an image net-img in our Host created from a Dockerfile:

/\*

FROM ubuntu:15.04

RUN apt-get update && apt-get install -y iputils-ping traceroute

ENTRYPOINT \["/bin/bash"\]

\*/

When I run two different containers out of the image generated from this Dockerfile:

\- docker run -it ---name=net1 net-img

\- docker run -it ---name=net2 net-img

If we type

\- brutal show docker0

// We now see two ids under the Interfaces tab that shows up. Correct

From this we can learn that, by default, each new container gets one interface automatically attached to the docker0 bridge

Let\'s go inside the net1 running container now...

\- ip a

We will see our network config form inside the container:

-   lo

-   eth0

    -   The ether is on the 172.17.0.4/16 adapter (16 bit socket mask)

**When the docker daemon starts on our host and it creates the docker0 virtual bridge, it assigns an IP address or (network address) as defined in RFC1918. It pretty much tries to get a network ID that isn\'t already in use by anyone else around.**

By default we should be able to ping the internet:

\- ping 8.8.8.8

We can also determine the container default gate-way if we trace route to the internet:

\- traceroute 8.8.8.8

So: 172.17.0.1 is our default gateway. It is the address of our Docker0 interface on the docker host.

Let\'s look how this eth0 inside of the container and the vethx interface we saw connected to the virtual bridge earlier how they work. SIMPLE

[Think of them as two ends of a Pipe]{.underline}

A good way to think of this is like a virtual ethernet cable. One end of the cable is plugged into the eth0 in the container, and the other end is plugged into the vethx port on the Docker0 bridge

![](007_08_-_Docker_Deep_Dive_-_Docker_Networking_000.png){width="5.0in" height="2.8in"}

 

**Network Configuration Files**

After doing some House Cleaning work on our Ubuntu host, let\'s quickly spin up a container to use for this demo\...

Using the net2 we spin before.... let\'s type:

\- docker inspect net2

// Here we see the NetworkSettings area and check out a lot of relevant info. Notice the Gateway: 172.17.42.1. All containers on this HOST will get the same default gateway. Which will be the address of our docker0 interface in the HOST namespace.

If we now try something like:

ls -l /var/lib/docker/containers/

// Remember this is where all of our container METADATA files live.

If we do /contianers/

We will get a handful of files.** For now we only care for:**

**     - hosts**

**     - resolve.conf**

resolve.conf looks exactly how we would expect it to look like! We have got a single DNS server: googles used and abused 8.8.8.8 and if we CAT the file we will get the resolve.conf file from the Docker HOST. Kinda looks the same...Well, by default, resolve.conf for every container of the HOST is a straight copy of the results.conf file form the HOST that is running on. [Though, we can override both of the values in resolve.conf on the docker run command line]{.underline}. 

What about the hosts file....No surprises either. IPV4 and IPV6 name resolutions.

With recent versions of Docker it is actually allowed to edit these two files on the fly while the container is UP and running....BUT be warned though: any changes we make like this will only persist while the container is running. They do not persists container restarts.

How can we overwrite these default settings?

\- docker run ---dns=8.8.4.4 ---name=dnstest net-img

\- docker inspect dnstest

// Here we go

How come, if we can base multiple containers out of a single image, how come each container can have it\'s own resolve.conf and hosts files. Well, behind the scenes every container gets it\'s very own resolves.conf and host files overload overlaid over the top of the resolves.con and host files that exist in the image and therefor the UNION file system of the container. So these files exist inside of the image when we spin up of the container but then on top of them we overlay new files.

**Exposing Ports**

The most common and the most basic way to allow basic communication between containers and to the outside world is by exposing ports from our containers

Let\'s take a look at a new Dockerfile:

/\*

FROM ubuntu:15.04

RUN apt-get update && apt-get install -y iputils-ping traceroute apache2

EXPOSE 80

#What this is doing is exposing PORT 80 from our container to our HOST

ENTRYPOINT\["apache2ctl"\]

CMD \["-D", "FOREGROUND"\]

\*/

After building an image out of this Dockerfile we will spin up a container off of that image\...

docker run -d -p 5001:80 ---name=web1 apache-img

-   -p = To expose ports

-   5001:80 = Map port 5001 on our Docker Host to port 80 on our Container, and vise versa as well. Meaning, any connections coming in to our host on port 5001 will be fowled to port 80 in our container. MAGIC

\- docker ps

// BOOM. Works

Now let\'s go to the browser. Now the container is running on our Ubuntu host here in the lab and the instructor got NameResolution setup so that that resolves to ubuntu1404.docker.course

If we just leave it like that (which will then take the default port: port 80) we see that there is nothing there. Remember that we are on the docker host here. But now, if we add the port 5001 tot he end:

ubuntu1404.docker.course:5001

// BOOM, we are in business

**Viewing Exposed Ports**

A good way to see ports in docker is with 

\- docker port

TCP or UDP?

By default, port mapping are assumed to be TCP, but Docker does let us map to UDP ports by slapping UDP onto the end of the -p switch

\- docker run -d -p 5002:80/udp ---name=web2 apache-img

What we are doing is pretty much launching a separate container this time called web2 and we are mapping its port 80 to an UDP port 5002 on the docker host.

Now this time if we do

\- docker port

result: 80/udp -\> 0.0.0.0:5002

// All the 0.0.0.0 refers to ALL the IPV4 addresses in our docker host.

Let\'s look at what IP addresses we have available in our docker host

\- ip -f init a

We are only interested in eth0 and eth1\...

This is showing us interfaces with an IPV4 address here on the docker host. This time let\'s go with the one 10.0.2.15

So let\'s say that we just wanted our containers port 80 to be exposed on port 5003 on our docker HOST but ONLY against the IP address 10.0.2.15.

\- docker run -d -p 10.0.2.15:5003:80 ---name=web3 apache-img

\- docker port web3

// 80/tcp -\> 10.0.2.15:5003

*[One last thing:]{.underline}*

We can use the -P (capital P switch): This will map all exposed port on a container (all ports marked as exposed in our Docker file) to random high number ports on the docker host.

Let\'s say our Dockerfile had: EXPOSE 80 500 600 700 800 900

\- docker run -d -P ---name=web4 apache-img

\- docker prot web4

500/tcp -\> 0.0.0.0:49159

600/tcp -\> 0.0.0.0:49160

700/tcp -\> 0.0.0.0:49161

80/tcp -\> 0.0.0.0:49162

800/tcp -\> 0.0.0.0:49163

900/tcp -\> 0.0.0.0:49164

All of our exported ports marked to random on our docker host.

**Linking Containers**

There is another common way of linking containers. A technology that Docker calls: Linking Containers. On the plus side Linking containers is way more secure than exposing ports the way we have been doing so far, but on the DOWN side, it only works with container to container communication. NOT with communicating with the outside world.

Theory:

When dealing with linking containers we need to understand that we got a source, and a recipient receiver. First, we fire up the source container (which is built from an image that got certain ports declared as exposed in the Dockerfile that was used to create the image) but we don\'t need to expose those ports at RUNTIME when the container is launched. So, they are not mapped to ports on the docker host...so, not available to the outside world.

Then we spin the recipient container, and when we do this we create a LINK back tot he source. At this point, the source tells the recipient various things about its networking config...IP address, protocols, ports and the likes.... and this info gets stored inside the recipient container. This means that the recipient container has the knowledge of the source container networking config and can each it and communicate with it. But all, without any ports on the source having to be exposed.

![](007_08_-_Docker_Deep_Dive_-_Docker_Networking_001.png){width="5.0in" height="2.8333333333333335in"}

Work:

\- docker run ---name=srcContiner -d img

// If we check that the container is running we can see that we get a 80/tcp under PORTS. This is just telling us that port 80:it\'s defined in the image assign exposed. Notice it is actually not listed as mapped to the docker host

\- docker run ---name=rcvrContianer ---link=srcContainer:ali-src -it ubuntu:15.04 /bin/bash

-   ---link = This is how we define the link back to the Source Container. We give the link the name of the source container, and an alias....like a Nickname. Both of these fields are **Mandatory.** They can be the same, but we are naming it ali to better understand.

//Boom now we got our two container linked.

\- docker inspect rcvrContainer

// We can see the Link from the recipient to the source.....

If we check the source though, there is no mention of the link from the source to the recipient. Remember we said the source populated the target with a bunch of networking information, lets see what that looks like:

\- docker attach rcvrContainer

\- env

// The source provides the receiver with a bunch of environment variables.

\- env \| grep ALI

// Ok so we now get a bunch of variables container details of the source container IP address and exposed ports in the likes.

Docker also adds an entry to the recipient containers HOSTS file. This maps the alias names back to the IP address of the source. (MAGIC).

-   This is more secure than exposing ports (no ports exposed here). In theory only the recipient container knows about the source container networking config

-   The recipient container can take this values and it can use them to dynamically and problematically configure itself.

**We can link MULTIPLE recipient containers to a SINGLE source container. And a SINGLE recipient container to MULTIPLE sources**

![](007_08_-_Docker_Deep_Dive_-_Docker_Networking_002.png){width="5.0in" height="2.7333333333333334in"}
