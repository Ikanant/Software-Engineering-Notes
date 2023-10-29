Creating Deployments

Sunday, April 18, 2021

10:24 PM

*So during the introduction notes I wrote about deployments and replica-sets... Within this notes I plan to go a bit into more detail in the notes bellow. After going over Pods, we were able to understand how to create these pods and how to manage the health of a given container using Probes... BUT this only helps us with failing containers... what happens when something is going wrong with the Pod itself... or if something/someone deletes the set Pod? \-\--\> We need to figure out the solution to this problem bellow.*

 

![Deployment Container ReplicaSet Container pod Container ](002_Creating_Deployments_000.png){width="7.783333333333333in" height="2.8916666666666666in"}

 

During the Introduction notes I wrote about the instance in which running

**Kubectl run \[containerName\] \--image=\"\[imageName\]\"**

Was able to NOT ONLY create a pod and have a running container inside of it... BUT ALSO it would have created a Deployment automatically for us. Sadly that automation is not default on the latest version of Kubernetes so make sure you know this if you played with it before.

 

**ReplicaSet: \"**[A ReplicaSet is a declarative way to manage Pods\"]{.underline}

*Following the analogy from the beginning, we can think of the ReplicaSet as the set of instructions (as our conductor) to handle if something is off with one of our Pods.*

 

***Deployment: \"***[A Deployment is a declarative way to manage Pods using a ReplicaSet\"]{.underline}

*In the evolution of Kubernetes, ReplicaSets came BEFORE deployments.*

 

 

![Pods represent the most basic resource in Kubernetes Can be created and destroyed but are never re-created What happens if a Pod is destroyed? Deployments and ReplicaSets ensure Pods stay running and can be used to scale Pods pods, Deployments, and ReplicaSets Pod Container ](002_Creating_Deployments_001.png){width="7.925in" height="3.091666666666667in"}

 

ReplicaSets essentially are going to control the Pod

 

![ReplicaSet Container ](002_Creating_Deployments_002.png){width="1.6166666666666667in" height="1.2in"}

 

ReplicaSets act as a Pod **controller:**

-   Self-healing mechanism.

    -   If you delete a Pod with a ReplicaSet or Deployment behind then it can magically be recreated for us.

-   Ensure the requested number of Pods are available

-   Provide fault-tolerance

-   Can be used to scale Pods (horizontally)

-   Relies on a Pod template

-   **No need to create Pods directly!**

-   Used by Deployments

 

![Result of Creating a ReplicaSet 2 Pods created iMac---3: replicaSets danwahlin\$ k get all + kubectl get all NME pod/ f rontend-8rs lg pod/ f rontend---zc8g I NME service/kubernetes NME READY 1/1 1/1 TYPE STATUS RESTARTS Running O Running O CLUSTER-IP AGE 8s Cluster1P 10.96.0.1 DESIRED CURRENT rep licaset. apps/ f rontend 2 2 EXTERNAL-IP READY AGE 2 PORT(S) AGE 443/TCP 41d ReplicaSet created ](002_Creating_Deployments_003.png){width="6.883333333333334in" height="3.3833333333333333in"}

 

So I am personally confused at this point... how do Deployments fit into this process?!

 

![Deployment ReplicaSet ](002_Creating_Deployments_004.png){width="2.283333333333333in" height="1.9916666666666667in"}

 

They are really a higher level wrapper around ReplicaSets. ReplicaSets use controllers to \*control the Pods... Deployments just make that process even easier.

 

A Deployment manages Pods:

-   Pods are managed using ReplicaSets

-   Scales ReplicaSets, which scale Pods

-   Support zero-downtime updates by creating and destroying ReplicaSets

    -   POWERFUL

-   Provides rollback functionality

-   Creates a unique label that is assigned to the ReplicaSet and generated Pods

-   The YAML for Deployments look VERY similar to the ones for ReplicaSets...

 

**Let\'s get started:**

The nice thing about YAML files for Deployments is that they already take care of creating the ReplicaSet for us. They are going to run behind the scenes and ensure that we have the right number of pods running. As we mentioned, Deployments are just a higher level wrapper that will take care of that for us.

 

![Definin apiVersion: apps/vl kind: Deployment metadata : spec : selector : template : spec : containers: a Deplo - name: my-nginx image: nginx:alpine ment (From a High-Level) Kubernetes API version and resource type (Deployment) Metadata about the Deployment Select Pod template label(s) \< Template used to create the Pods \< Containers that will run in the pod ](002_Creating_Deployments_005.png){width="6.866666666666666in" height="3.5416666666666665in"}

 

*Extra Notes:*

-   *apiVersion*

    -   *Kinda sucks. In order to know what goes here we need to look into the Kubernetes documentation*

-   *Kind*

    -   *Earlier We had kind: Pod... If we were creating a ReplicaSet it would be kind: ReplicaSet.*

-   *Metadata*

    -   *We can define the name of the deployment... as well as any labels we would like to add*

-   *Spec*

    -   *Notice how we have one here and one bellow... What we are doing is that we are defining one spec here for the deployment and another for the pod*

-   *Selector*

    -   *It is going to define what template we will be using. Normally it goes right bellow but it can also be in a separate file. Ultimately what this is going to use is select the template the has the Pod spec (which is the spec right bellow it)*

-   *The second spec is essentially what we already covered in the Pods module*

 

Check out a more detailed Deployment YAML:

![apiVersion: apps/vl kind: Deployment metadata : name: frontend labels : app: my-nginx tier: frontend spec : selector : matchLabe1s : tier: frontend template : metadata : labels : tier: frontend spec : containers: - name: my-nglnx image: nginx:alpine Kubernetes API version and resource type (Deployment) Metadata about the Deployment \< The selector is used to \"select\" the template to use (based on labels) Template to use to create the Pod/Containers (note that the selector matches the label) ](002_Creating_Deployments_006.png){width="6.716666666666667in" height="3.575in"}

 

![](002_Creating_Deployments_007.png){width="6.725in" height="3.675in"}

 

 

**Hands On Time**

*The way to get a Deployment created is very similar to what we already saw with PODS... which means the rules we established earlier about **create** vs **apply** also apply :)*

 

**Kubectl apply -f file.deployment.yml**

Will allow us to add changes later on to our resource

 

**Kubectl create -f file.deployment.yml \--save-config**

Adding the save config will allow us to add changes as well. Both options work.... People often just go with **apply** to be safe.

 

**Kubectl get deployment** *(or deployment)*

Will get us the list of all existing Deployments

 

**Kubectl get deployment \--show-labels**

Will show us the labels with the existing deployments

**-l switch** can help us filter by just the deployments with a specific label

**Kubectl get deployment -l app=nginx**

 

**Kubectl delete deployment \[deployment-name\]**

Deleting a deployment means it will also delete ALL associated Pods/Containers

 

**Kubectl scale deployment \[deployment-name\] \--replicas=5**

Can also use yaml file

**Kubectl scale -f file.deployment.yaml \--replicas=5**

We can ALSO specify the replicas in the yaml file btw:

![spec : replicas: 3 selector : tier: frontend ](002_Creating_Deployments_008.png){width="3.1333333333333333in" height="1.75in"}

 

 

*Jumping into the example provided by the course:*

![nginx.deployment.yml X Samples \> Deployments \> nginx.deploymentyml \> { ) spec \> { ) selector \> {)matchLabels \> üapp 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 apiVersion: apps/vl kind: Deployment metadata: name: my---nginx labels: app: my---nginx spec : selector: matchLabels : app: my---nginx template: metadata: labels : app: my---nginx spec: containers: --- name: my---nginx image: nginx:alpine ports: --- containerPort: 80 resou rces : limits: memory: \"128M\" #128 MB cpu: \"200m\" #200 millicpu 1 (.2 cpu or of the cpu) ](002_Creating_Deployments_009.png){width="7.433333333333334in" height="6.783333333333333in"}

 

*The Selector is what is a bit burry at the moment. Here we are matching labels for \"app\" with value \"my-nginx\"... now this is confusing because I also have the same label for the metadata of the Deployment itself but that doesn\'t matter really... because inside of the metadata for the actual Pod... we also have \"app\" with value \"my-nginx\"*

 

![21 24 resources limits: memory : \"128Mi\" #128 MB \"200m\" #2ØØ millicpu cpu; (.2 cpu or of the cpu) ](002_Creating_Deployments_010.png){width="5.3in" height="1.0333333333333334in"}

 

*The extra piece of info here about the resources of a Pod is important. This allows us to constrain what a given container is allowed to run inside of a Pod. This is important in case a container goes off and potentially take down even an entire Node.*

 

*If I wanted to shell INTO the container in the POD the command has been updated... an example would be:\
***kubectl exec -it \[PodName\] \-- sh**

 

 

We can get the list of deployments with any of the following commands really:\
 

![danwahlin\$ + kubectl get deploy NAME READY UP-TO-DATE 1/1 1 my---ngxnx danwahtin\$ + kubectl get deployment NAME READY UP-TO-DATE my---nginx 1/1 1 danwahtin\$ + kubectl get deployments NAME READY UP-TO-DATE my---nginx 1/1 1 iMac---3:Deployments danwahlin\$ k k k 1 get deploy AVAILABLE AGE 1 1Ø7s get deployment AVAILABLE AGE 1 1Ø9s get deployments AVAILABLE AGE 1 112s ](002_Creating_Deployments_011.png){width="5.375in" height="2.825in"}

 

 

*If by any chance I wanted to show the LABELS for the Deployments and/or Pods... I\'d simply type:\
***kubectl get pods \--show-labels**

 

*While playing around with Labels and the selector for our Deployment I found out that something like this:\
* 

![one 7 8 9 10 11 12 13 14 15 16 17 18 19 20 orange : spec selector : matchLabe1s : basic-deployment -fancy app : apple: two template : metadata labels app: basic-deployment apple: two spec containers : fancy-container-name name image: nginx: alpine ](002_Creating_Deployments_012.png){width="5.033333333333333in" height="3.575in"}

*Would not work for us... since the matchlabels need to match ALL of the labels in there..... Now in the other hand:*

![spec : selector : matchLabe1s apple: two template : metadata : labels : app: basic-deployment apple: spec : ](002_Creating_Deployments_013.png){width="3.408333333333333in" height="2.4166666666666665in"}

*That would work! - Cool!*

 

**[HOW DO WE SCALE?]{.underline}**

![danwahtin\$ k scale ---f nginx.deployment.ymt ---replicas=4 + kubectl scale ---f ng inx. deployment . yml ------replicas=4 deployment. apps/my---nginx scaled 1 iMac---3: loyments danwahlin\$ ](002_Creating_Deployments_014.png){width="7.675in" height="1.0in"}

 

**Kubectl scale -f \[yaml file\] \--replicals=\[# of replicas we want\]**

 

Or we can introduce this in the YAML file itself...

 

![Windows PowerSheII PS E: k get all NAME pod / basic -deployment- 657b9c9c7f -5xj pf pod / basic -deployment -657b9c9c 7f -v898w READY 1/1 1/1 STATUS RESTARTS Running Running EXTERNAL-IP PORT(S) NAME service/kubernetes NAME TYPE ClusterIP CLUSTER-IP 10.96.ø.1 READY 2/2 -657b9c9c7f \< none) 443/TCP AVAILABLE AGE 31s 31s AGE 3Øh AGE 31s deployment. apps / basic -deployment NAME replicaset. apps / basic -deployment UP-TO-DATE 2 DESIRED 2 2 CURRENT 2 READY AGE 2 31s PS E: \\Workspaces\\KubernetesTraining\\Dep10yments\> k delete deployment -1 orange=\"one deployment. apps \"basic-deployment\" deleted ](002_Creating_Deployments_015.png){width="7.158333333333333in" height="3.1666666666666665in"}

ALSO notice how we can delete using the labels

 

SUMMARY:

![kubectl kubectl kubectl kubectl kubectl kubectl create -f nginx. deployment.yml - -save-config describe \[pod I deployment\] \[pod-name I deployment-name\] apply -f nginx.pod.yml get deployments \--show-labels get deployments -1 app=my-nginx scale -f nginx.deployment .yml - - replicas=4 ](002_Creating_Deployments_016.png){width="9.225in" height="2.825in"}

 

 

 

**Deployment Options**

*All through the notes above we can see how Deployments can help get up and running with our Pods in our cluster, there is a lot of things we can do as well...*

 

![Current Pod Container nginx:I.14.2-alpine Change Image Desired Pod Container nginx:I.15.9-aIpine ](002_Creating_Deployments_017.png){width="6.175in" height="1.7166666666666666in"}

*Let\'s say we currently have an update to whatever application we have running inside a container inside a Pod... (Like for example the nginx application we have been using till just now)... in the old days to accomplish something like this we would probably end up having to stop the old container and then bring up the new one... potentially even having a down-time for our application... Deployments allows us to solve this problem! WHAT?!*

 

[Zero downtime deployments allow software updates to be deployed to production without impacting end users.]{.underline}

This is a GIANT topic and there should probably be another full courses on this subject... but let\'s see what the options that are out there and how they can help us developers...

 

-   One of the strength of Kubernetes is zero downtime deployments

-   Update an application\'s Pods without impacting end users

-   Several options are available

    -   (default) Rolling updates

    -   Blue-Green deployments

        -   We are all familiar with this... we only bleed customers over once we know for SURE that we are ready to go.

    -   Canary deployments

        -   We bleed a small number of customers at time

    -   Rollbacks

        -   Tried it and it didn\'t work... let\'s go back to the previous version

 

**Rolling Deployments**

*The way rolling deployments work is simple... let\'s say we have our application running across 4 PODS.... Once we have an update to our application we essentially stand up ONE POD.... And once it is ready (we can test using Probes) we can remove one of the old Pods that has the outdated application... and so on and so on...*

 

*You know what\'s cool? - If we simply run a **kubectl apply -f file.deployment.yml** this automatically happens!*

 

**ACTION TIME**

*To allow for more progress in the course I only payed attention to this chapter: 4:7.... If necessary I will include it in the DEMO... it would be cool... but it worked extremely similar to what we saw above... can I make a quick Abrigo Vue App container? Sure can!*

 

*The only thing to note from the DEMO is that we used Services... which will be on the next Chapter... it will be even cooler looping back to this module once I understand how those work.*
