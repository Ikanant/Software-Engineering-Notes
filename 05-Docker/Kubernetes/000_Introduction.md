Introduction

Sunday, April 18, 2021

1:33 PM

**Overview**

*In this notes I am going to write down everything Kubernetes related FROM A DEVELOPERS perspective. Why do we \*as developers\* want to learn Kubernetes? What benefits do we get from learning about it?*

Official Definition: [Kubernetes (8s) is an open-source system for automating deployment, scaling, and management of containerized applications.]

The real question, at least for me, is how is Kubernetes any different than docker-compose for example... in which we write a .yaml file that contains the configuration of our docker containers and allows us to run different commands on them like *docker-compose up/down* from the terminal? - Well, docker compose was never intended to be used in a production setting... but let\'s assume we do... what happens if we require to scale our application(s)? What happens when one or more of our running containers fail?

![It Would Be Nice if We Could\... Package up an app and let something else manage it for us Not worry about the management of containers Eliminate single points of failure Scale containers Update containers without bringing down the application Have robust networking and persistent storage options ](000_Introduction_000.png)

All of the things above can be done by using Kubernetes... or in other words (like the ones I am sure you have heard off) Kubernetes is a tool to orchestrate docker containers... like a conductor would in an actual orchestra. The conductor knows who is playing music when, when they should start and stop... or even if they need to replace a musician for another at some point during the show.

![Key Kubernetes Features Service Discovery/ Load Balancing Self-healing Storage Orchestration Secret and Configuration Management Automate Rollouts/Rollbacks Horizontal Scaling ](000_Introduction_001.png)

... these are NOT the only tools Kubernetes does for us BUT, these are some of the main ones we often focus on as developers when working with Kubernetes.

**The Big Picture**

Kubernetes started out at Google... There was a need within the company for container and cluster management... they used it for OVER 15+ years... WHAT?! I don\'t think it was called kubernetes back then but this certain is what we know and love today.

Some people see Kubernetes at the core: As a bunch of state machines

Kubernetes moves you to a desired state....

![Current State Container Kubernetes Desired State Container Container ](000_Introduction_002.png)

So you can start with a certain state, and if you wish to change it somehow, that\'s what Kubernetes can help you to do... like a GPS map... it will take you from point A to point B.

**Core components:**

-   **ONE or more of MASTER nodes**

    -   Boss of the operation that knows how to manage it\'s different employees that are our worker nodes. Worker nodes can be physical servers, virtual machines (more often than not)... and together they create a CLUSTER.

    -   The MASTER will start something on EACH of this nodes called **POD.**

-   **PODS**

    -   Are essentially a way to host a container. POD itself is essentially the package (or the box really) for the product... so if you go to the store and pick something up, you are not going to run the box itself... you are going to get the box and run whatever is inside of this box. We can have MANY pods for a given machine. Similar to having multiple containers in a machine... This is where horizontally scaling becomes a more clear possibility

    -   They DON\'T EXISTS on their own... we need some other lego pieces to support them. While we can have many pords running containers across a Kubernetes cluster we are going to need something to deploy them...

        -   **ReplicaSet**

    -   We also need the pods to communicate to the outside world or even just among themselves within a cluster...

        -   **Service**

            -   Different types of resources that can be used to make sure our pods are being deployed properly, that they are running, the containers within them are healthy, etc

-   **Node**

    -   Just a machine (or more commonly a Virtual Machine) that can run one or more PODS as mentioned. The way our MASTER node can communicate to the worker nodes is by utilizing:

        -   **Store (etcd)**

            -   Think of it as the Database that the master node needs to track everything

        -   **Controller Manager**

            -   Responsible for when a request comes in, the manager can act upon that request accordingly and schedule it for action... which leads us into:

        -   **Scheduler**

            -   Will determine WHEN the NODES actually come alive, or go away or whatever action we have sent to our controller

        -   **API Server**

            -   SO, how do WE as developers/DevOps/SysEng can interact with the master node? This is done by using a command line tool called: **\$kubectl**

                -   People call it: CubeCTL / CubeCuddle / CubeController

            -   Just a command line tool that we can send requests into the master which then can be sent into the cluster.

            -   Ultimately this tool is [simply], as far as I know, making RESTful service calls to send our BEFORE/AFTER state request to the master.

                -   We can use YAML or even JSON metadata files to send these requests

        -   **Kubelet**

            -   Each node, in addition to having each POD running... it also \*needs a way to communicate back and forth to the master so it has a little AGENT installed that\'s running on each node. This is known as kubelet.

        -   **Container Runtime**

            -   Need to run our containers within the PODs

        -   **Kube-Proxy**

            -   Networking Capabilities of course are REQUERIED. So Kube-Proxy allows us to ensure that each POD has a unique IP address

![The Master Node Store (etcd) API Server Node Pod Master Node Pod Cluster Controller Manager Scheduler Node Pod ](000_Introduction_003.png)

![Pod Container Pod Container Pod Container ](000_Introduction_004.png)

![Pod Deployment ReplicaSet Pod Container Service Pod Container ](000_Introduction_005.png)

![Node Kubelet Container Runtime Pod Container Pod Kube-Proxy Container ](000_Introduction_006.png)

*Of course there are more pieces that form the complex tool that is Kubernetes, BUT as far as basics goes... the pieces above are the CORE elements that will allow us to hit the ground running when setting things up.*

**Benefits and Use Cases**

*Why do we even care about any of this? As developers I don\'t often deal with the production setup, networking or servers or anything like that... even when using the cloud there are tons of options that will run containers for me... so WHY?*

[Well, lets start by reminding ourselves the benefits of using docker containers to begin with:]

-   Accelerated Developer Onboarding

    -   If taking advantage or docker and docker-compose we can stand up an entire environment up and running easily for new-hires or even people that just got brand new laptops

-   Eliminate App Conflicts

    -   We are capable of running different versions of the same app very easily

-   Environment Consistency

    -   Our code TRULLY works on my machine but also on staging/uat/production

-   Ship software faster

[Now let\'s think of the Kubernetes benefits:]

-   Orchestrate containers

-   Zero-Downtime deployments

    -   Think of our Blue/Green deployment strategy... let\'s take it up and notch

-   Self Healing

    -   This is like a super power, we can have Kubernetes handle when a container is faulty and it will replace/remove/update it without dev intervention

-   Scale Containers

    -   If we want more PODS with containers on a given node, with a single command we can do this

[Developer Use Cases:]

-   Emulate production locally

-   If we move as a company to use Kubernetes, it will be extremely important that we are all familiar with how things work

-   Create an end-to-end testing environment

    -   Let\'s say we want to bring the EXACT environment from production

-   Ensure application scales properly

    -   How do we know if this would ever work if we can\'t replicate in our local machines

-   Ensure secrets/configs are working properly

    -   We recently dealt with this by moving some of the SWA configuration key/value pairs to our config.json file... that works great, but it doesn\'t cover secrets... do we really need to keep asking devops for those?

-   Performance testing scenarios

    -   We might want to see what our limits are in a cluster. How do scale out for these challenges?

-   Workload Scenarios (CI/CD and more)

    -   We can even use Kubernetes for our build servers... Maybe we have MULTIPLE builds across different products we release... and we want to use this with docker containers... (we already moved in that direction for applications like Resources allowing us to play with different node versions across these builds and utilizing the power of volumes)

-   Learn how to leverage deployment options

    -   Use industry patterns like Canary Testing, A/B or Blue/Green testing

-   Help DevOps create resources and solve problems

    -   As a problem comes up on PROD, as developers we might need to troubleshoot what is actually going on... if we don\'t know anything about Kubernetes that is going to be challenging.

-   ...

**Running Kubernetes Locally**

There are tons of options out there to get started...

-   Minikube

    -   <https://github.com/kubernetes/minikube>

    -   Been around for a long time

    -   Limitations: You can\'t scale out like a Production instance of Kubernetes

    -   It will provide **kubectl** as well as ONE MASTER / WORKER node to test things with

-   **Docker Desktop \<\-- ONE I ARE GOING TO USE**

    -   <https://www.docker.com/products/docker-desktop>

    -   By far the easiest to get started with

    -   Same limitations as Minikube. No scalability and ONE MASTER / WORKER nodes

    -   Allows for rest of normal kubernetes to have multiple pods / deployments / service / etc

    -   Seems like this is something that is included (but unchecked by default) when installing Docker in your local\>

-   Kind

    -   <https://kind.sigs.k8s.io>

    -   Will allow you scale out in your local machine.

-   Kubeadm

    -   <https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm>

    -   Allow you to install the FULL Kubernetes.

    -   This is more targeted towards administrators of a Kubernetes cluster

**Getting Started with kubectl**

![\$kubectl Node Pod Master Node Pod Node Pod ](000_Introduction_007.png)

![Getting Started with kubectl Commands kubectl version kubectl cluster-info kubectl get all kubectl run \[container-name\] - image-name\] kubectl kubectl kubectl kubectl port-forward \[pod\] \[ports\] expose create \[resource\] apply \[resource\] Check Kubernetes version View cluster information Retrieve information about Kubernetes Pods, Deployments, Services, and more Simple way to create a Deployment for a Pod Forward a port to allow external access Expose a port for a Deployment/Pod Create a resource Create or modify a resource ](000_Introduction_008.png)

[Quick tip:]

In Powershell: Set-Alias -Name k -Value kubectl

One that it is not fully specified above is that we might end up using **kubectl get pods** to get all the pods in our worker machine.

**K create / apply** are our most common actions for creating/change/modify a resource.

**Web UI Dashboard**

*This is totally optional... but it will give me a chance to play with some of the commands we saw above and will allow us to inspect things better. To enable it do:*

-   **Kubectl apply -f \[dashboard-yaml-url\]**

    -   Apparently this url has change through the years... but similar how we are going to do things later, we are essentially passing in a yaml metadata file that will get us sorted out for the UI in our local. You can check out the kubernetes docs for the latest yaml file link:

        -   <https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/>

    -   As of 4/18/2020 it is:

        -   <https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml>

-   **Kubectl describe secret -n kube-system**

    -   We need a TOKEN to be able to login locally. We need to find that token so we can login. The command above will add a token to a special place of Kubernetes and as an administrator we can get to that token.

    -   Locate using: kubernetes.io/service-account-token

    -   Today the service we care about is at the very top... so just scroll up and copy token

    -   ![Data ca.crt: kube metes . io/ service- account -token 1066 bytes namespace: 11 bytes oken : eyJhbGci0iJSUz11Ni1s1mtpZC161kN0d28zcXB4YWhtYU11NktWkdrekktT2g1VIBLS05mVmpPbUNaS2pEeFkifQ. eyJpc3Mi0iJ lcm51dGV zL3N1cnZpY2VhY2NvdW501iwia3ViZXJuZXR1cy5pby9zZXJ2aWNIYWNjb3VudC9uYW11c3BhY2UiOiJ ILXN5c3R1bS1s1mt1YmVybmVOZXMuaW8vc2Vydm1jZ FjY291bnQvc2VjcmVOLm5hbWUiOiJhdHRhY2hkZXRhY2gtY29udHJvbGx1ci10b2t1bi13N2tqYy1s1mt1YmVybmvozxmuaW8vc2Vydm1jZWFjY291bnQvc2Vydm1 jZS1hY2NvdW50Lm5hbWUiOiJhdHRhY2hkZXRhY2gtY29udHJvbGx1ci1s1mt1YmVybmVOZWuaW8vc2Vydm1jZWFjY291bnQvc2Vydm1jZS1hY2NvdW50LnVpZC161 mNhZTMzNjYOLTNjNTgtNDY2Zi1hMzczLTNhODYzMzQ3NTczMC1s1nNIYi161nN5c3R1bTpzZXJ2aWNIYWNjb3VudDprdWJILXN5c3R1bTphdHRhY2hkZXRhY2gtY29 udHJvbGx1ciJ9.Y9MhiJygQLtbdm6EQn-s1xenbS15bWzOJtkOTk8UmymY72SPe09URQ3F-Tz4NZzzmJjUZXeD7cu01haON8AZ7V2vRCtMxDi u9EMRon2GOu1VQty I hXK4T95CHZL03Y6i7n3DK AubN64CEC01t1Z5h7VF-QJZtHC1chhZuB3Gae6GYDvq1D-smudc1A J9ERGIGnQe9Bs7i8DpsNh2DppYmKSnETt2pRfHtLy6jftpoS6X pCPjxViQGEfxGG025pSiF17c1gf8QXhWJD8QTd20t2t3rxoxG PW-AiSbGA3nADtr1cTRJPHgouBj5BBSB-41erRDMBOGne-TCN15sg ](000_Introduction_009.png)

-   **Kubectl proxy**

    -   Create proxy so we can open and get too that particular application in our kubernetes cluster

    -   Once we run this, we will have an service running under port: 8001... and we need to use the link provided in the documentation link above to get to our login screen. Today the link was:

> <http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/>
>
>  

-   **Visit the dashboard with the URL and LOGIN using the token**

> ![O kUbernetes Overview Cluster Cluster Roles Namespaces Nodes Persistent Volumes Storage Classes Namespace default Overview Workloads Cron Jobs Daemon Sets Deployments Jobs Pods Replica Sets Replication Controllers Stateful Sets Discovery and Load Balancing Ingresses Services Config and Storage Config Maps Persistent Volume Claims Secrets Custom Resource Definitions Settings About Q Search Discovery and Load Balancing Services Name kubernetes Config and Storage Secrets Name default-token-4hz7x Namespace default Namespace default Labels component: apiserver provider: kubernetes Labels Internal Cluster IP Endpoints kubernetes:443 TCP 10.96.0.1 kubernetes:o External Endpoints TCP Type -10f1 Created 33 minutes ago Created 33 minutes ago kubernetes.io/service account-token -10f1 ](000_Introduction_010.png)
>
>  

*Keep close attention to all of the options we have on the left hand side nav bar. Everything should be empty but we now have access to Nodes / Pods / Jobs and more... This is a helpful way to see what resources we have available.*

*Party time... time to create some PODs*
