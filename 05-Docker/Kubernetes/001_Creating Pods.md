Creating Pods

Sunday, April 18, 2021

4:21 PM

*At this point I have already gone over the fact that PODS can essentially be the host of our containers... Dan Wahlin had a nice analogy about them being a space suit... inside the suit an astronaut is capable of not only communicating with base control through some microphone inside the suit, but also report back all sorts of vitals information about the stage of a mission... PODS are something like that.. A bit beyond being just a box for our containers.*

*By the end of this page, we should be able to be familiar with PODs core concepts, how to create a pod and YAML Fundamentals. Instead of using a more imperative approach (do things through kubectl) to more of a declarative approach (do things through yaml file which is run through kubectl)... ALSO: Pod HEALTH \<\-- very important :)*

![Deployment ReplicaSet Pod Container Pod Container Service Pod Container ](001_Creating_Pods_000.png)

Kubernetes Definition: [A Pod is the basic execution unit of a Kubernetes application-the smallest and simplest unit in the Kubernetes object model that you create or deploy.]

I like to think of Kubernetes as a bunch of Legos that allow us to build complex structures... a Pod is a basic building block.

It is important to think of Pods as the way to organize the different parts of our applications. This is most likely going to influence the way we write our dockerfiles that will create the containers and what type of code we put in them... Normally we have a single application per container AND more often than not we will have a single Container per Pod (Though Pods can host more than one).

![Kubernetes Pods Node Pod Container Pod Container Smallest object of the Kubernetes object model Environment for containers Organize application \"parts\" into Pods (server, caching, APIs, database, etc.) Pod IP, memory, volumes, etc. shared across containers Scale horizontally by adding Pod replicas Pods live and die but never come back to life ](001_Creating_Pods_001.png)

*Notice the last point... this relates to the Pods health mentioned above*

![Master Node Pod ](001_Creating_Pods_002.png)

![Node Pod Container Pod Container ](001_Creating_Pods_003.png)

Inside our worker nodes our Pods can be horizontally scaled... which means that we can create Pods replicas... which are copies of the pods which Kubernetes can Load Balance between those... If one of the Pods has some issue... Kubernetes can automatically take it out and put something back something healthy.... By doing so Kubernetes is NOT bringing back to life a bad Pod... The Pod that caused problems is REMOVED and a NEW one is brought to life.

Pods within a NODE are going to have their own distinct IP address AND containers within those Pods are going to have their respective PORTs... The IP addresses are known as a CLUSTER IP Addresses. [SO Pods containers share the same Network namespace!] AND Pod containers are going to talk to one another using loopback network interface (localhost) which should be the fastest way to accomplish this.

Containers within the SAME Pod NEED to have a different port of course.

![Node Pod Container Port 80 10.0.0.43 Pod Container Port 80 10.0.0.53 ](001_Creating_Pods_004.png)

Ports can be reused by containers in separate Pods

**Pods do NOT span nodes**

![Node Pod Container Node Pod Container ](001_Creating_Pods_005.png)

Doing something like the image above is quite complicated and not-useful

**Creating a Pod**

*Let\'s start simple*

There are various ways to create a Pod, but the most straight forward way (Imperative as we described above) is just running:

**Kubectl run \[podname\] \--image=nginx:alpine**

*Of course there are other flags that can be passed in the run command BUT this is already enough to get me started with a Pod running a docker container from the image specified.*

![\# List only kubectl get \# List all kubectl get Pods pods resources all Get Information about a Pod The kubectl get command can be used to retrieve information about Pods and many other Kubernetes objects ](001_Creating_Pods_006.png)

When a Pod is brought to life is going to get its very own Cluster IP address... This just means this IP address is ONLY exposed to the nodes to the Pods within a given Cluster and it is NOT accessible outside of the cluster...

What do we do if we brought up nginx OR asp.net Core OR Java.... And now we want to test that locally into Kubernetes Docker Desktop or MiniKube or whatnot? We will need to expose the Pod PORT to be able to get to it:

**Kubectl port-forward \[name-of-pod\] 8080:80** *for example*

Looks familiar? This is resembles the same way we deal with ports in docker

![Internal port \# Enable Pod container to be \# called externally kubectl port-forward \[name-of-pod\] 8080:80 External port ](001_Creating_Pods_007.png)

A Pod can also be easily deleted by doing something like:

**Kubectl delete pod \[name-of-pod\]**

*Note that:*

-   *Running a Pod will cause a Deployment to be created*

-   *To delete a Pod use kibectl delete pod or find the deployment and use kibectl delete deployment*

**IN OTHER WORDS:** (This is important) When deleting a Pod directly, I often get confused when I later check all the pods that exists running the **get pods** command and HEY, the Pod I deleted is still there! Does this mean the delete command didn\'t work? This is when looking closely into the ID of the Pod is beneficial... the ID is different! What this means is that when I deleted the Pod, Kubernetes went ahead and created a new Pod again for us... because REMEMBER, Kubernetes wants to KEEP you at the current state you are AT... If you want to REALLY delete the Pod, you will need to delete the Deployment that originally scheduled the Pod.... (I will cover that in a future page)

**NOW THIS IS THE WHERE THE FUN PART BEGINS:**

![Windows PowerSheII PS C: Set-Alias PS C: k get all Falcon and Winter Soldier F X k ---Name le.96.e.1 kubectl Docker Desktop for Mac a F localhost:1 234 O o \'000\' X Web UI (Dashboard) Kube X Kubernetes Dashboard Finances Photography Gig Video x Welcome to nginx! NAME service/kubernetes TYPE Cluster IP CLUSTER-IP EXTERNAL \<none\> - -image=nginx : alpine -IP PORT(S) 443/TCP diaServer Audio Software Documentation 74m PS C: k run my-first-pod pod/my-first-pod created PS C: k get pods NAME my-first-pod READY 1/1 STATUS RESTARTS Running e PS C: k get services Welcome to nginx! If you see this page, the nginx web server is successfully installed and working. Further configuration is required. For online documentation and support please refer to nginx:ocg. Commercial support is available at nginx.com. Thank you for using nginx. NAME kubernetes TYPE CLUSTER-IP EXTERNAL-IP PORT(S) Cluster IP le.96.e.1 \<none\> 443/TCP 76m PS C: k port-forward Forwarding from 127.e.e.1:1234 8e Forwarding from \[::1\]:1234 -\> 80 Handling connection for 1234 Handling connection for 1234 my-first-pod 1234: 80 ](001_Creating_Pods_008.png)

Zoomed in:

![Windows PowerSheII PS C: Set-Alias PS C: k get all NAME service/kubernetes TYPE Cluster IP k kubectl ---Name CLUSTER-IP EXTERNAL-IP le.96.e.1 \<none\> PORT(S) 443/TCP 74m PS C: k run my-first-pod pod/my-first-pod created PS C: k get pods - -image=nginx : alpine NAME my-first-pod READY STATUS RESTARTS Running e 1/1 PS C: k get services NAME kubernetes TYPE CLUSTER-IP EXTERNAL-IP Cluster IP le.96.e.1 \<none\> PORT(S) 443/TCP 76m PS C: k port-forward my-first-pod 1234: 80 Forwarding from 127.e.e.1:1234 8e Forwarding from \[::1\]:1234 -\> 80 Handling connection for 1234 Handling connection for 1234 ](001_Creating_Pods_009.png)

*This is very unlikely to be the way we do things at Abrigo... or anywhere really... this is just a basic fun way to showcase how things are running behind the scenes*

*Note: When we load the service... notice that we have the cluster IP... could we have hit that from the browser instead of localhost? NO -\> Remember that cluster Ips are internal only! We essentially just poke a hole in Kubernetes to access the content/container inside that Pod...*

*Note2: Notice that running the port-forwarding command locks up the console which would force us to either stop the task OR open up another console instance.*

![1.18+ \"run\" only creates the Pod \< 1.18 \"run\" creates the Pod and other resources ](001_Creating_Pods_010.png)

*Turns out the note above is outdated... because Kubernetes no longer creates a deployment when running a simple run command. Interesting*

**YAML Fundamentals**

*Did you know that YAML means: Yet Another Markup Language? Now it is known as YAML Ain\'t Markup Language (official terminology)... weird.*

-   YAML files are composed of maps and lists

-   Indentation matters

-   **Always use spaces**

-   Maps

    -   name: value pairs

    -   Maps can contain other maps for more complex data structures

-   Lists

    -   Sequence of items

    -   Multiple maps can be define in a list

![key: value complexMap : keyl : value key2 : subKey: value items : - iteml - item2 itemsMap : - mapl : value maplProp: value - map2: value map2Prop: value \< YAML maps define a key and value \< More complicated map structures can be defined using a key that references another map \< YAML lists can be used to define a sequence of items \< YAML lists can define a sequence maps Note: • Indentation matters • Use spaces not tabs ](001_Creating_Pods_011.png)

*Before jumping into creating Pods using YAML files know that this is also NOT the standard way of doing things... more to come about that.*

![apiVersion : kind: Pod metadata : name: my-nginx spec : containers: - name: my-nginx image: nginx:alpine Kubernetes API version \< Type of Kubernetes resource Metadata about the Pod \< The spec/blueprint for the Pod Information about the containers that will run in the pod ](001_Creating_Pods_012.png)

*This is an example of YAML file that would do 100% of what we already went over using the **kubectl run** command*

To create a pod using YAML I just need to use the **create** command along with the\--filename or -f switch

**Kubectl create -f file.pod.yml \--dry-run \--validate=true**

-   *Validation is the default... which would yield errors if yaml is invalid... but we can do validate to false in some cases*

-   *Dry-run will do a trial run of sorts... Instead of potentially affecting the cluster... we can try the command and see what it\'d generate in the output.... From there we can run it*

Once I am ready to run the command FORREAL!

**Kubectl create -f file.pod.yml**

*Note: Remember that what is happening behind the scenes is that we are taking the information from that yaml file and sending it UP to the API service of our master node which then gets converted and stored inside of the master which will start the scheduling process by the controller...*

*What happens if we run this command and the particular resource already exist?*

By default: Error... though there are simple ways to make it so that we replace the Pod we are trying to create

**ALTERNATE (TWO STEP PROCESS)**

Use the **apply** action using the same yml file... This is more preferable almost ALWAYS... because this will Create a resource same as before BUT ALSO Update a resource if it already exists...

![\# Alternate way to create or apply changes to a \# Pod from YAML kubectl apply -f file. pod .yml Store current properties in resource\'s annotations \--save-config when you want to use \# Use \# kubectl apply in the future kubectl create -f file. pod .yml - -save-config ](001_Creating_Pods_013.png)

-   *\--save-config*

    -   *Create some annotations so when we do apply later, it will take whatever we are trying to APPLY and compare it to what is there in the first place and overwrite specific settings.*

    -   ![apiVersion : kind: Pod metadata : annotations : kubectl. kube rnetes . io/ last-applied-configu ration : { \" apiVersion \" : \"VI \" , \"kind\" : \" Pod \"metadata \" : { \" name\" : \" my-nginx\" \--save-config causes the resource\'s configuration settings to be saved in the annotations Example of saved configuration Having this allows in-place changes to be made to a Pod in the future using kubectl apply ](001_Creating_Pods_014.png)

There are OTHER options too.... There is a

-   **kubectl edit**. This will allow me to EDIT the file for the specified resource right in the console

-   **kubectl patch**. This will let me patch a particular property

If in the future I want to delete Pod but don\'t know it\'s name... we can also use the source yaml file to accomplish this:\
![\# Delete Pod kubectl delete pod \[name-of-pod\] \# Delete Pod using YAML file that created it kubectl delete -f file. pod.yml ](001_Creating_Pods_015.png)

**Putting things into practice\
** 

![Pods \> 1 2 3 4 5 6 7 8 9 10 11 12 13 ! basic-pod.yml apiVersion: VI kind: Pod metadata name: my-cool -nginx labels: app: nglnx rel: stable spec containers : name: my-cool-nginx nginx: alpine Image ports containerPort: 8 ](001_Creating_Pods_016.png)

*I just want to not here that I am adding a metadata property here called [labels.] Currently these labels are not doing anything... BUT we can use these labels to link resources to each other, whether they are pods, deployments or even services.*

If we run the yaml file above, and THEN run the command: **kubectl get pod \[pod-name\] -o yaml** (or json) We will get back a super long description of the Pod that is currently running.... That also includes some *[annotations]* These annotations is what the \--save-config did.... It added the current version of the yaml (converts it to json internally)... so if I ever make modifications (like changing the image) Kubernetes would compare the version of the image that it currently has and overwrite accordingly

*-o means Output*

![\'S E: \\Workspaces\\KubernetesTraining\\Pods\> apiVersion: VI Kind: Pod netadata : annotations : k get pod my-cool-nginx -o yaml kubectl. kubernetes. io/last-applied-configuration: I { \" apiVersion\" : \"VI \" , \" kind\" : \"Pod\" , \"metadata\" : { \" annotations\" : { } , \" labels\" : { \" app\" • \"nginx\" , \" rel \" : \" stable\"}, \"name\" : \"my-cool -nginx\" , \"namespace\" : \"default\"} \' \' 301 -nginx\" , \"ports\" : \[ {\"containerport\" : creationTimestamp : labels: app: nginx rel: stable managedFie1ds : - apiVersion: VI \'spec\' \' : {\"containers\' \' : \[ image\" : \"nginx : alpine\" , \"name\" : \"my- ](001_Creating_Pods_017.png)

Another way to get info about our Pod is using the **Describe** command

Among some other information that comes up whenever we run the command, it is really cool to take a look at the bottom of the logs... where we have the Events section.

![Windows PowerS PS E: \\Workspaces\\KubernetesTraining\\Pods\> k describe pod my-cool-nginx Name : Namespace : Priority: Node : Start Time: Labels: Annotations : Status : IPs: my-cool-nginx default e docker-desktop/192.168.65.4 sun, 18 Apr 2e21 -e4ee app=nginx rel=stable \<none\> Running le.1.e.9 le.1.e.9 Containers : my-cool-nginx: Container ID: Image : Image ID: Port : Host Port: State : Started : Ready : Restart Count: Environment : Mounts : docker : / /5ad8eee5991e336fcbcad3a5389d36ca54633fbbe2681a7c134c4e6f63ee63fa nginx : alpine : e7ab71a2c8e4ecb19a5a5abcfb3a4f175946cee1c8af288b1aa766d67bede5d2 8e/TCP e/TCP Running sun, 18 Apr 2e21 True e \<none\> -e4ee /var/run/secrets/kubernetes.io/serviceaccount from default-token-4hz7x (ro) Conditions : Type Initialized Ready ContainersReady PodSchedu1ed Volumes : Status True True True True default -token -4hz7x: Type : SecretName : Optional : QoS Class: Node -Selectors : Tolerations : Secret (a volume populated by a Secret) default-token-4hz7x false BestEffort \<none\> node. kubernetes. io/not-ready:NoExecute op=Exists for 3ees node. kubernetes. io/unreachab1e:NoExecute op=Exists for 3ees Events : Type Normal Normal Normal Normal Reason Scheduled Pulled Created Started Age 6m56s 6m55s 6m55s 6m55s From default-scheduler kubelet kubelet kubelet Message Successfully assigned default/my-cool-nginx to docker-desktop Container image \"nginx:alpine\" already present on machine Created container my-cool-nginx Started container my-cool-nginx PS E: \\Workspaces\\KubernetesTraining\\Pods\> ](001_Creating_Pods_018.png)

These list of Events will show different failures that can occur with our Pod. This is [very] useful to troubleshoot issues

Notice that when I run the apply command now it says that nothing has changed... cool!\
![Windows PowerSh PS E: \\Workspaces\\KubernetesTraining\\Pods\> pod/my-cool-nginx unchanged PS E: \\Workspaces\\KubernetesTraining\\Pods\> k apply . \\basic-pod .yml ](001_Creating_Pods_019.png)

**NOW EVEN COOLER**

If we wished to jump inside the container itself, we can do this VERY similarly to how we do it on a docker container... *BTW notice that if we run docker ps we will see the containers that we have started through these notes...*

![PS E: \\Workspaces\\KubernetesTraining\\Pods\> k exec my-cool-nginx kubectl exec \[POD\] \[COMBAND\] is DEPRECATED and will be removed MAND\] instead. -it sh in a future version. Use kubectl exec \[POD\] - .COM ](001_Creating_Pods_020.png)

**AND LAST BUT NOT LEAST FOR DELETING**

![PS E pod PS E : \\Workspaces \\KubernetesTraining\\Pods\> \"my-cool-nginx\" deleted : \\Workspaces \\KubernetesTraining\\Pods\> k delete . \\basic-pod. yml ](001_Creating_Pods_021.png)

*BOOM!*

***Pod Health***

*Kubernetes relies on [Probes] to determine the health of a Pod container.*

**Probe:** A diagnostic performed periodically by the kubelet on a container. This for sure affects us as developers... since technically we should be the ones that know the most about what is actually happening inside that container and therefore we can write the probe.

There are two types:

1.  Liveness Probe

    a.  Check if the Pod is alive and how is it doing

2.  Readiness Probe

    a.  Helps Kubernetes to know WHEN should the Pod start sending/getting requests

Reminder: Failed Pod containers are recreated by default (restartPolicy defaults to Always)

If the container in the Pod FAILS one of the checks mentioned above, similarly it can be restarted.

How can we write these tests and checks? There are tons of ways and they really depend on the application/service that lives in the container itself... We can:

-   ExecAction

    -   Executes an action inside the container. Run a command which as long as it returns zero is successful.

-   TCPSocketAction

    -   TCP check against the container\'s IP address on a specified port

-   HTTPGetAction

    -   HTTP GET request against a container. (More commonly for us)

Probes only have 3 possible results:

-   Success

-   Failure

-   Unknown

**Liveness Probe Example:**

Let\'s assume we are dealing with an API of some sort.. Or even nginx ... One of the best ways to know things are working is by sending a request and ensuring we get the result we expect... like a static file or something... As a developer, this is a great opportunity to write some sort of API call within our very own tool, that the kubelet can call into!

![](001_Creating_Pods_022.png)

This is a BIG deal! Why?! Because as developers WE are now going to define what determines if our service is healthy or NOT... not just a random check of dashboard in NewRelic (great anyway of course)

Another great example straight from the Kubernetes documentation:

![Defining an ExecAction Liveness Probe apiVe rsion : kind: Pod spec : VI containers : - name: liveness image: k8s .gcr. io/busybox a rgs : - /bin/sh - touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; livenessProbe: exec : command : - cat - /tmp/healthy initialDe1aySeconds: periodSeconds: 5 sleep 600 5 Define args for container \< Define liveness probe \< Define action/command to execute ](001_Creating_Pods_023.png)

In the example above we are simply defining some args that are going to run when we spin up our container... we are going to shell inside, do a command, we are going to toucha file called health, sleep 30 seconds after that\'s created, then we are going to REMOVE (rimraf) of that healthy file and then we are going to sleep for another 600 seconds.

What our Liveness probe is going to do is TRY to get to that healthy file and that will determine if our container is alive or NOT... Of course it is going to be alive for the first bit of the age of the container but after a bit when the file gets deleted, then our probe would fail.... Which for us will AUTOMATICALLY bring up a new container with the same initial delay and a period of seconds for which it checks.

**Readiness Probe Example:**

![](001_Creating_Pods_024.png)

In the example above we are essentially doing the exact same check as the one above for our health page BUT... but a readinessProbe does is it will hold traffic to this node UNTIL the probe is successful.

![Readiness Probe: When should a container start receiving traffic? Liveness Probe: When should a container restart? ](001_Creating_Pods_025.png)

![](001_Creating_Pods_026.png)

![](001_Creating_Pods_027.png)

So the screenshot above is freaking awesome! Essentially we are just running a simple nginx container... which as many of us know has a default index.html file that is served as a sign that the service is running... What we defined in our yml file is that IF when running an HTTP GET request to the service we DO NOT receive a 200 http code back... then we are going to fail our livenessProbe... which by default just means we have the pod restarted... in the example we even got kicked out of our shell due to the container being shut down... now.... Why is it still there when we run the get pods command? Easy! Kubernetes just rested it for us!\... AWESOME

*BTW: You can force the deletion of a Pod by using:\
* 

**kubectl delete pod \<PODNAME\> \--grace-period=0 \--force \--namespace \<NAMESPACE\>**
