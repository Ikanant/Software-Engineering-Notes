HashiCorp Documentation

Tuesday, March 24, 2020

1:20 PM

**Intro**

 

\*\*\* This notes assume I\'ve properly downloaded and installed Consul on my machine. For every node that runs consul we will be having the binary just run in the background. Make sure that the consul command is accessible from the terminal by checking our System Variables and point one to the binary.

 

After a succesful installation we need to run Consul in **either** SERVER or CLIENT mode. Each DC (datacenter) most have at least ONE server. [A single SERVER deployment is HIGHLY discouraged.]{.underline}

 

All other agents run in client mode. A CLIENT is a very lightweight process that:

-   Registers services

-   Run health checks

-   Forwards queries to servers

 

The agent HAS to be running on EVERY node that is part of the cluster.

 

For simplicity we can run a node in development mode in our local machines. This is useful to get up and running quickly with Consul. It is NOT intended to be used in Production as it DOES NOT persist any state.

 

**consul agent -dev -node machine**

 

The consul agent will start and output log data for this. By default here the agent will be running automatically in SERVER mode and it will take leadership of the cluster.

 

If we run

**consul members**

 

We will see the list of members in the consul cluster. Additional metadata can be viewed with the

**-detailed**

 

Note that this output is using the GOSSIP protocol and it is \*\*eventually consistent. So this can have a minor delay and might NOT see the actual current state of servers.

 

For a STRONG feedback use the http api:

**curl localhost:8500/v1/catalog/nodes**

 

Beyond the API, the DNS interface can be used to query the node. Note that you HAVE to make sure to point your DNS lookups to Consul agent DNS server which runs on port 8600 by default.

 

**dig \@127.0.0.1 -p 8600 machine.node.consul**

 

Side Note: Refer to here to install the tool dig (Domain Information Groper)\
<https://help.dyn.com/how-to-use-binds-dig-tool/>

 

The easiest way to shut down the consul agent is by CTRL-C

This is considered a graceful exit and consul will go ahead and notify the other members of the cluster about the node that just left.

 

Forcing an exit will make the other members register that original node as FAILED.

-   When a member leaves it services and checks are REMOVED from the catalog

-   When a member fails.. It\'s health gets set to CRITICAL but it is NOT removed from the catalog

    -   Consul will continue to try to reconnect these failed nodes

    -   If a SERVER node is removed, this will potentially lead to a service outage which is NO BUENO

 

**consul leave**

Is also the other option to run on the server to stop the consul node from running. I think this can make all nodes running on

 

 

**Register a Service and Health Check**

 

A Service can be registered either by providing a service definition (MOST COMMON WAY) OR by making a call to the HTTP API. Consul loads ALL configurations files in the configuration directory.

 

Service definition configuration file. Let\'s look at the following line:

![\[II rails\"\], \"port\": echo \"web\" \"tagsll: I {\"service\" : name ](000_HashiCorp_Documentation_000.png)

 

\^\^\^ Let\'s pretend we have a service named \'web\' running on port 80. We will give it a TAG that we can use as an additional way to query the service \'rails\'

Now let\'s restart the agent providing the configuration directory... I created consul.d because that is the conventional way to create a directory with config files in UNIX.

 

**consule agent -dev -config-dir=./config.d -node=machine**

 

By doing this we SYNCED the web service... which means we loaded the service definition from the configuration file and registered in the service catalog. We are essentially free to create however many services as long as we create their respective service definition files in the configuration directory.

 

Once we are done and we have the agent running, we are good to query the new service either by the DNS API or the HTTP API.

For using the DNS API just know that we can get it from the \<nameOfService\>.service.consul (using the proper ip of course)

**dig \@127.0.0.1 -p 8600 web.service.consul**

 

By DEFAULT all of the DNS names are always in the consul namespace (though this can be changed)

 

![, flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: WAN\'IING: recursion requested but not available o, ADDITIONAL: 2 , OPT PSEUDOSECTION: EDNS: version: 0, flags: ; QUESTION SECTION: ; web. service. consul. ANSWER SECTION: web. service. consul. , ADDITIONAL SECTION: web. service. consul. Query time: 0 msec , SERVER: udp: 4096 IN IN IN TXT 127.0.0.1 \"consul-network-segment=\" ; WHEN: Wed Nov 14 PST 2018 MSG SIZE rcvd: 99 ](000_HashiCorp_Documentation_001.png)

 

From here NOTE that we get an A RECORD was returned with the IP of the node where this service is available.

A RECORDS can only hold IP addresses. We can use the DNS API to get the entire address port pair though:

**dig \@127.0.0.1 -p 8600 web.service.consul SRV**

 

AND the other way to query these services is by using the TAG... meaning we can do: \<tagName\>.\<serviceName\>.service.consul

**dig \@127.0.0.1 -p 8600 rails.web.service.consul**

\^\^\^ HERE we are querying Consul (our server) to yield ALL services with RAILS tags... regardless of what node they are on.

 

[Now for HTTP:]{.underline}

**curl <http://localhost:8500/v1/catalog/service/web>**

 

The catalog API will yield all the nodes using the given service. The problem here is that this will return ALL nodes hosting the given service...NOT just the healthy ones (which is what the DNS api is doing under the hood)... to filter things up just

**curl \'<http://localhost:8500/v1/catalog/service/web?passing>\'**

 

Service Definitions CAN be changed !!! We can do this by configurations files AND sending SIGHUP to the agent... this let\'s you update services WITHOUT any downtime.

**consul reload**

\^\^\^ will do the SIGHUP for us

 

The HTTP API can also be used to add/delete/edit services dynamically.

 

**Connect Services**

 

![Sidecar Proxy App 1 TLS 1 Sidecar Proxy App 2 ](000_HashiCorp_Documentation_002.png)

 

Consul also provides a feature called CONNECT. This will allow to automatically connect services and nodes through an automatically-encrypted TLS connection that will also set the authorization of which services are allowed to connect to each other. Applications do NOT need to be modified AT ALL to use CONNECT...

Sidecar proxies can be used to automatically stablished TLS conenctions for in/out bound connections without being aware of connect at all. Though applications can ALSO use CONNECT natively for optimal performance and security.

 

Starting out with a consul server node:

**consul agent -dev -config-dir=./consul.d -node=machine**

 

Now let\'s start a SERVICE that\'s 100% unaware of CONNECT... let\'s start a SOCAT to start a basic ECHO service... this will take TCP connections and echo back any data sent to it

(This is in UNIX only service)

**socat -v tcp-l:8181, fork exec:\"/bin/cat\"**

 

Now this socat service is running in the background on port 8181 and we can connect to it easily by

**nc 127.0.0.1 8181**

 

Now every text sent in the console is gonna be echoed back. This will not have any encryption or fancy tasks. We can think of this as our (unaware of CONNECT) Database or Back-End web service.

 

We can register this new service with consul easily by adding another service definition... same as what we just did above BUT this time we will also configure CONNECT

 

![\"service\" : \"name\": \"socat\", \"port\": 8181, { \"sidecar_service\": \"connect\" : ](000_HashiCorp_Documentation_003.png)

 

[The empty configuration we have provided here notifies consul to register a sidecar proxy for this process. The proxy process represents the specific service that accepts INBOUND connections in a dynamically allocated PORT. Verifies and authorizes TLS connections and proxies back a standard TCP connection to the process.]{.underline}

 

... TO BE CONTINUED

 

 

**Create a Local Consul Datacenter**

 

Now time for the big picture:

![Static Host-based networking O Dynamic Service-based networking ](000_HashiCorp_Documentation_004.png)

 

When a consul agent starts up, it has NO idea about any of the other nodes. It is isolated cluster of ONE. To learn about other cluster members, it just needs to join an existing cluster...

 

In order for a node to enter an existing cluster it only needs to know about a SINGLE existing member... (SERVER or CLIENT). After it joins, they will gossip with one another and quickly discover the other members in the cluster. To simulate a MORE realistic cluster I will start 2 node cluster via Vagrant

 

<https://github.com/hashicorp/consul/tree/master/demo/vagrant-cluster>

 

Using the vagrant file provided by the Hashicorp we will setup TWO agents that can stood up simply by running

**vagrant up**

 

More info on Vagrant:

[Vagrant in 5 minutes](https://www.youtube.com/watch?v=wlogPKBEuUM)

 

![VAGRANT ](000_HashiCorp_Documentation_005.png)

[Docker Vs Vagrant](https://www.youtube.com/watch?v=9QGkJvbLpRA)

 

![LXC Easier to cr ](000_HashiCorp_Documentation_006.png)

 

 

We can SSH into them by simply running

**vagrant ssh \<nameOfNode\>**

 

From with the node we can then spin up a consul agent. This time around we can\'t simply just flag it out as -dev in a clustered environment... This is where we now start specifying our flags manually:

**consul agent -server -bootstrap-expect=1 -data-dir=/tmp/consul -node=agent-one -bind=172.20.20.10 -client=172.20.20.10 -enable-script-checks=true -config-dir=/etc/consul.d -ui**

 

-   -node

    -   Each node in a cluster must have a unique NAME

    -   By default consul uses the host name of the machine

-   -bind

    -   This is the address that Consul listens on and it must be accessible by other nodes in the cluster

    -   This is NOT strictly necessary BUT Consul will by default attempt to listen on ALL IPv4 interfaces but will FAIL to start with an ERROR if multiple private IPs are found

        -   Since Production servers often have multiple interfaces, specifying a BIND address assures us we won\'t run into trouble.

-   -server

    -   Will make this node a server

-   -bootstrap-expect

    -   Hints to the consul server the number of expected of additional server nodes we are expecting to JOIN.

-   -enable-script-checks

    -   This will enable health checks that can execute external scripts

-   -config-dir

    -   Mark where the service definition can be found

 

**consul agent -data-dir=/tmp/consul -node=agent-two -bind=172.20.20.11 -enable-script-checks=true -config-dir=/etc/consul.d**

-   -bind

    -   Address to match the IP of the second NODE as specified in the Vagrant file

 

At this point these TWO servers still don\'t know anything about each other... and are part of their own single node cluster.

**consul members**

\^\^\^ verify

 

Now we will tell the first agent to join the second agent

**consul join 172.20.20.11**

\^\^\^ This works.... AWESOME !!!

 

Ideally, whenever there is a new node added in our datacenter it should automatically join the Consul cluster without human intervention. This is can be done by enabling auto-discovering of instances in AWS, Google Cloud or Azure with a given TAG and key value.

 

 

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

Curl -X PUT -d \'jonathan.hernandez@gmail.com\' <http://localhost:8500/v1/kv/swa/local/LocalDeveloperEnvironmentEmailAddress>

Curl -X PUT -d \'weakLocalPassword\' <http://localhost:8500/v1/kv/swa/local/LocalDeveloperEnvironmentEmailPassword>

Curl -X PUT -d \'true\' <http://localhost:8500/v1/kv/swa/local/ShowConsulTile>

Curl -X PUT -d \'jonathan.hernandez@gmail.com\' <http://localhost:8500/v1/kv/swa/stg/LocalDeveloperEnvironmentEmailAddress>

Curl -X PUT -d \'strongLocalPassword\' <http://localhost:8500/v1/kv/swa/stg/LocalDeveloperEnvironmentEmailPassword>

Curl -X PUT -d \'false\' <http://localhost:8500/v1/kv/swa/stg/ShowConsulTile>

 

**consul-template -template=\"webAppSettings.config.tpl:webAppSettings.config\" -once**

 

**consul agent -server -bootstrap-expect=1 -data-dir=/tmp/consul -node=agent-one -bind=172.20.20.10 -enable-script-checks=true -config-dir=/etc/consul.d**

**consul agent -data-dir=/tmp/consul -node=agent-two -bind=172.20.20.11 -enable-script-checks=true -config-dir=/etc/consul.d**

**consul agent -ui=true -retry-join=172.20.20.10 -advertise=127.0.0.10 -data -dir=/tmp/consul -node=localMachine**

 

{{ \$ENVIRONMENT_NAME := \"/swa/local\" }}\<appSettings\>

> \<add key=\"LocalDeveloperEnvironmentEmailAddress\" value=\"{{key_or_default (print \$ENVIRONMENT_NAME \"/LocalDeveloperEnvironmentEmailAddress\") \"tasdases\"}}\" /\>
>
> \<add key=\"LocalDeveloperEnvironmentEmailPassword\" value=\"{{key_or_default (print \$ENVIRONMENT_NAME \"/LocalDeveloperEnvironmentEmailPassword\") \"dsas\"}}\" /\>
>
> \<add key=\"ShowConsulTile\" value=\"{{key_or_default (print \$ENVIRONMENT_NAME \"/ShowConsulTile\") \"\"}}\" /\>
>
> \<add key=\"ConsuleNodeCount\" value=\"{{ len nodes }}\" /\>
>
> {{ if (len nodes) gt 5 }}\<add key=\"ConsuleNodeCount\" value=\"{{range nodes}} {{.Address}};{{end}}\"/\>{{end}}

\</appSettings\>

 
