Overview

Saturday, March 21, 2020

7:43 PM

 

**Challenge:**

Let\'s take into consideration the way a load balancer works. The user makes a request to a load balancer and proceeds to get router to the \*right web server that\'s going to return data to the user. This is pretty straight forward. The thing to note now is... how does the load balancer KNOW about these servers? The answer is **Service Discover.**

 

Beyond that, the load balancer also needs to know whenever the server that is pointing our users too is available and running... otherwise we might lead costumers towards a broken site...this is called **Failure Detection.**

 

What about if our application is using multiple services that are deployed across various cloud providers or data centers? We still need to handle that

 

![Challenges Service Service Discovery Failure Detection Multi Datacenter Configuration ](001_Overview_000.png)

 

 

Consul is a tool that provides the answer to more than one question... For us, the only thing we care about is the Service configuration side of things. How can we maintain and deal with configuration variables across all of our environments.

 

As we move to a more microservice type approach, we simply can\'t rely on manual intervention to change config files. For this issue Consul also provides a distributed key/value store... This can be used to be able to store configuration to our application.. We can also rely on writing data to a fault tolerant key/value store.

 

This key/value store is reactive. It could watch for change (not only for services)... Let\'s say we store our application configuration inside of this key/value store and we perform a change...this change can then be pushed into our RUNNING application.

 

**Reactive Configuration via Key/Value Store**

 

![haproxy.cfg docker 4 Consul Template K/v lb (172.20.20.11) haproxy.ctpml Services Catalog ](001_Overview_001.png)

 

 

![80 lb (172.20.20.11) docier PROXY 8080 8080 8080 webl (172.20.20.21) NGMX--- web2 (172.20.20.22) NGMX öocEQr web3 (172.20.20.23) consul-server (172.20.20.31) desky (172.20.20.1) ](001_Overview_002.png)

 

Looking at the above diagram we have to understand that Consul works (very similar to Octopus) in two modes... SERVER mode and CLIENT mode... in our system I am going to setup a single SERVER node and go from there...

 

Above we have:

-   Server node

-   Local node (my laptop)

-   Load Balancer node

-   3 WFE nodes

 

To get things started we will use Vagrant to spin up all the VMs that we will use in this lecture... I am not going to dive deep into the tools it uses but essentially we can look into the following diagram.

 

![VAGRANT Creating VMS wesmcclure/ubuntu1404-docker consul-server ](001_Overview_003.png)

 

 

 

Vagrant will pull down the image wesmcclure and spin up a VM using virtual box

 

 

*vagrant init \--minimal wesmcclure/ubuntu1404-docker*

Running this command will create a vagrant file. Vagrant file is what describes a VM.

 

Inside the vagrant file we will need to define multiple VMs... the first one of which will be our consul SERVER.

 

![Vagrantfile X Vagrantfile Vagrant. configure( \"2\") do I configl config. vm. box \"wesmcc1ure/ubuntu14e4-docker\" config.vm. define \"consul-server\" do I CSI cs .vm.hostname = \"consul-server\" cs .vm.network \"private_network\", ip: \"172.2e.2e.31\" end end ](001_Overview_004.png)

 

This configuration is the one that will set things up for us for our server node. This node WILL have docker installed on it which will allow us to run nginx/hsproxy without much hassle.

 

*Vagrant box list*

This w command will show the boxes running on this computer as well as their version.

 

Now the thing to do is to INSTALL consul on this newly created node. This should be extremely simple...

1.  Download the file

2.  Unzip it

3.  Move the binary to somewhere where we can access it (put it in the path of our system)

 

We could ssh into the machine and accomplish the steps above easily... BUT we want to stay away from such manual labor if later on we will have to do the same to so many nodes... so mitigate this we will create an install.consul.sh script file.

 

**Side note:** When using Vagrant, our created nodes will have a vagrant folder that is shared behind the scenes by Virtual Box that links us to the root of our project. Meaning whatever files we declare in the root of our project will be available by any node kicked up with our Vagrantfile

 

*config.vm.provision \"shell\", path: \"install.consul.sh\", privileged: false*

 

I am also going to make sure we run the isntall.consul.sh file we just created when each node gets created SO.... Keep in mind that provision scripts will run only ONCE.

 

**Server mode**

 

Now on my new node running consul I need to specify that\'s a server mode...

*Consul agent -dev*

The dev flag will indicate that we are running in development mode on this agent. A development agent means we have the server mode running on this agent.

 

\^\^\^ alright... the above code is not going to work properly because Consul is now binding things automatically to localhost somehow... so I found that by specifying -bind flag that will allow us to set the ip address of our server inside our vm... command will look like

consul agent -dev -bind 172.20.20.31

 

This should get things running BUT it will not allow us to see the web-ui for the server since this one is running on the 127.0.0.1 ip of the VM.. So the best we can do is to curl and show text output... so now we are gonna spin up Consul on our local computer as another node AND we will run the consul agent on that as well and that agent will expose the web interface

 

![desky (172.20.20.1) consul-server (172.20.20.31) ](001_Overview_005.png)

 

 

So on our local we can run something along the lines of

 

*consul agent \--config-file local.consul.json*

Instead of setting up flags on this command, we can ALSO use config file

 

![local.consuI.Json \"ui\": true, \"retry_join\" \[\"172.2e.2e.31\"\], \" advertise addr : \" \"172.2e.2e.1\", \"data dir\" : \"/tmp/consul \" ](001_Overview_006.png)

 

1.  We set the ui flag to true. That enables consul web ui. We need this because we are NOT running on server mode

    a.  User interface is separate from api.. We don\'t need this to use the api

2.  Retry-join will allow us to specify the location of another node. This is the way we attach to our server node...

    a.  NOTE: This is a cool thing about consul...we do NOT need to provide the ip of the server node.. This can be any node in our cluster

3.  Advertise

    a.  Same as the server

    b.  We are saying the the console agent running on my local computer will be listening on that ip.

    c.  This is the ip address virtual box assigns to the local computer for this private network

4.  Data directory

    a.  In dev node there is no need for data_directory everything will be lost when we restart the dev server

 

![Nodes - Consul G) localhost:8500/ui/dc1/nodes O D ACL e Passing Checks Finances DESKTOP-SSG4UOA 172.20.20.1 Video Audio Software Documentation Images dcl Services Nodes Key/Value Intentions Nodes 2 total All (Any Status) Critical Checks Healthy Nodes consul-server 172.20.20.31 A Warning Checks ](001_Overview_007.png)

 

Things working nice and pretty now

 

**API**

 

In addition to this awesome web UI we can also take advantage of their HTTP API... so instead of hitting the server using the url above we can do:

 

Localhost:8500/v1/catalog/nodes

 

And that will return a json object for us to consume

<https://www.consul.io/api/catalog.html>
