Creating Services

Monday, April 19, 2021

10:13 PM

 

*As we deploy our Pods to our clusters, we obviously need to find a way to make them communicate with one another... ALSO, we need to make sure we can talk from the outside world into some of those pods. That is what services are all about.*

-   Service Core Concepts

-   Service Types

-   Creating a Service with kubectl

-   Creating a Service with YAML

    -   Which we will learn how to deploy with kubectl as well

 

![Deployment Container ReplicaSet pod Container Container Service ](003_Creating_Services_000.png)

 

***Service:*** [A Service provides a single point of entry for accessing one or more Pods.]{.underline}

*One important question to consider is.... Since Pods live and die.... Can we even rely in their IP addresses? Not really*

 

![External caller Front-end Pod Coma 10.0.0.43 Back-end Pod Cot&üer 10.0.0.45 ](003_Creating_Services_001.png)

*IP addresses change a lot... and so relying on it would not be a good idea.*

 

-   *Pods are \"mortal\" and may only live a short time (ephemeral)*

-   *You can\'t reply on a Pod IP address staying the same*

-   *Pods can be horizontally scaled... so each Pod gets its own IP address*

-   *A Pod gets an IP address [after]{.underline} it has been scheduled (no way for clients to know IP ahead of time)*

 

*The way this works is probably the way I already envisioned... we can have a SERVICE have a static IP address which will know how to talk to the services behind it.*

 

![my-app Pod Container my-app 10.0.0.43:80 Service 10.0.0.1:80 my-app Pod Container 10.0.0.53:80 ](003_Creating_Services_002.png)

*LABELS are going to be what we use to associate PODS with a SERVICE*

 

-   Services abstract Pod IP Addresses from consumers

-   Load balances between pods OUT OF THE BOX

-   Relies on Labels to associate a Service with a Pod

-   Node\'s kube-proxy creates a virtual IP for services

    -   Remember we mean our worker node here. As in the VM running all the pods

-   Uses Layer 4 (TCP/UDP over IP)

-   Services are NOT ephemeral

    -   They tend to stick around! Unlike Pods

-   Creates endpoints which sit between a Service and a Pod

 

![Calling Services External Service Caller 10.0.0.1:80 Pod Container 10.0.0.43:8080 fronten Pod Container 10.0.0.53:8080 Service 10.2.0.1:9000 Pod Container 10.2.0.10:27017 ](003_Creating_Services_003.png)

 

*Something really cool is described in the image above... even our Pods use services to talk to other Pods. Services are essential to stablish this communication.*

 

![](003_Creating_Services_004.png)

 

*AND REMEMBER, Services do the Load balancing out of the box for all of the Pods that are running with it... so as request come, it will manage dropping off these requests across the Pods that are ready to go.... AND FROM OUR LAST HANDS ON TALK ON THE PREVIOUS MODULE.... This is what also happens with the client\'s browser when accessing our application. Because browsers use the same connection over-over-over for the request to the server... that by default will be respected by Kubernetes and that means we will continue to use the same Pod behind the scenes... STICKY!*

 

***It is important to note that this is VERY VERY HIGH LEVEL... and courses ONLY on Services networking are probably required to really get a grasp of everything that can be done.***

 

**Service Types**

 

1.  ClusterIP

    a.  (default) Expose the service on a cluster-internal IP

        i.  Service IP is exposed internally within the cluster

        ii. Only Pods within the cluster can talk to the Service

        iii. Allows Pods to talk to other Pods

        iv. ![Cluster pod Container Service Container Service Container ](003_Creating_Services_005.png)

2.  NodePort

    a.  Expose the service on each Node\'s IP at a static port

        i.  Exposes the Service on each Workers Node\'s IP at a static port

        ii. Allocates a port from a range (default is 30000-32767)

        iii. Each Node proxies the allocated port

        iv. ![External Caller Node (port 30100) Service (NodePort) Pod Container Pod Container ](003_Creating_Services_006.png)

3.  LoadBalancer

    a.  Provision an external IP to act as a load balancer for the service

        i.  Exposes a Service externally

        ii. Useful when combined with a cloud provider\'s load balancer

            1.  Azure/AWS/etc... they will have their own version of a LoadBalancer and then K8s has it\'s own one as well (K8s can use NGINX - Default one - others)

        iii. NodePort and ClusterIP Services are created

        iv. ![Node (30105) LoadBaIancer Extemal Caller x.x.x.x:80 Node (30105) Service (NodePort) Service (NodePort) ](003_Creating_Services_007.png)

        v.  This kind of utilizes the other services we already went over... We have cluster IP services behind the scenes and nodePort services on the Nodes that are setup and then a LoadBalancer knows how to talk to those.

4.  ExternalName

    a.  Maps a service toa DNS name or IP address

        i.  Service that acts as an alias for an external service

        ii. Allows a Service to act as a proxy for an external service

            1.  Lets consider that our domain or IP keeps changing on us... and we need to keep updating the containers in the Pod that want to talk to it.... This is where proxy logic works.

        iii. External service details are hidden from cluster (easier to change)

        iv. ![Cluster Pod Service pod Container Service (ExternalName) External Service ](003_Creating_Services_008.png)

 

 

**ACTION TIME USING KUBECTL**

 

*So if we were to access a Pod from outside of Kubernetes... is that even possible... we have already gone over this... NOT really... because everything is setup as a cluster IP... the only way to accomplish this (and we already did it for a bit) is using PORT FORWARDING*

 

***Kubectl port-forward pod/\[pod-name\] 8080:80***

*Or even we can do it with a deployment*

***Kubectl port-forward deployment/\[deployment-name\] 8080***

*And the same can be done for a Service*

***Kubectl port-forward service/\[service-name\] 8080***

 

*When we do something like forwarding the pod above we are simply opening up the port 8080 that then proxys into the pod for us.*

 

**What is the difference between port forwarding with a Deployment/Pod?** I THINK it will forward and load balance for us.

 

**Creating a Service with YAML**

*This should be pretty straight forward.*

 

![apiVersion: VI kind: Service metadata : spec : type : selector : ports : Kubernetes API version and resource type (Service) Metadata about the Service \< Type of service (ClusterlP, NodePort, LoadBalancer) - defaults to ClusterlP \< Select Pod template label(s) that service will apply to Define container target port and the port for the service ](003_Creating_Services_009.png)

 

*Let\'s look at a SIMPLE example of a ClusterIP type service. The one thing to not is that OUR SELECTOR for the label will apply to Pods AND Deployments that match the labels*

 

 

![](003_Creating_Services_010.png)

 

**COOL COOL COOL ALERT \>\>\> The Name of the Service will get it\'s own DNS entry within the internal DNS in the Kubernetes cluster**

 

**ClusterIP Service Example**

*It is a clusterIP type when we DO NOT specify the type*

![apiVersion: VI kind: Service metadata : name: frontend apiVersion: VI kind: Service metadata : name: backend Name of Service (each Service gets a DNS entry) \< A frontend Pod can access a backend Pod using backend:port ](003_Creating_Services_011.png)

 

*SO SO SO in this case a front-end pod can simply access a back-end pod by using:*

**Backend:port**

Doing this will make our lives a million times easier because we won\'t need to worry about IP addresses

 

**NodePort Service Example**

![apiVersion: VI kind: Service metadata : spec : type: NodePort selector : app: nginx ports: - port: 80 targetPort: 80 nodePort: 31 øøø Set Service type to NodePort Optionally set NodePort value (defaults between 30000-32767) ](003_Creating_Services_012.png)

 

This NodePort is what we have been doing this WHOLE TIME... but now we just wrote it down in a YAML file

 

**LoadBalancer Service Example**

![apiVersion: VI kind: Service metadata : spec : type: LoadBa1ancer Set Service type to LoadBalancer (normally used with cloud providers) selector : app: nginx ports: - port: 80 targetPort : 80 ](003_Creating_Services_013.png)

 

**ExternalName Service Example**

Not as common... We are essentially creating an ALIAS.... In the example bellow we are calling it \"external-service\" which for any pod that wants to use this service, instead of having to go to the IP address or weird DNS.... It can just go to external-service (the name) and it will go to **api.acmecorp.com**

*So in the example bellow we would end up with:*

**External-service:9000**

 

![apiVersion: VI kind: Service metadata : name: external-service spec : type: ExternalName externalName: api . acmecorp.com ports: - port: 9000 Other Pods can use this FQDN to access the external service Set type to ExternalName Service will proxy to FQDN ](003_Creating_Services_014.png)

 

 

**Kubectl commands**

*This should be very familiar at this point...*

 

**kubectl create -f file.service.yml**

*It will be a ClusterIP by default because we did not specify the type... Now this service will pick up ANY of those Pods that might have been deployed, that might have the specific label... THEN remember we can use the NAME of the service to call from other Services/Pods*

 

**Kubectl apply -f file.service.yml**

*Again... apply will allow us to Create OR Update a service... and when it come to services they might be needed to get updated more often than we think... when working with BlueGreen or Canary type tests for example, things can be a bit more complicated.*

 

**Kubectl delete -f file.service.yml**

*Same as usual*

 

*HOW ABOUT: If we wanted to see if a Pod can call another Pod ??? How quickly can we test a service is working correctly?*

The answer will shock you... We can simply just exec to shell into the Pod/Container and send a [curl]{.underline} command against the Pod IP that we want to call.

 

**Kubectl exec \[pod-name\] \-- curl -s <http://podIP>**

*Do know that doing this and the curl command isn\'t available, we might need to just get it ready for us first...*

***Kubectl exec \[pod-name\] -it sh (OLD)***

***Kubectl exec -it \[pod-name\] \-- sh (NEW)***

-   ***apk add curl*** (of course this will depend on the type of linux running behind the scenes)

-   **Curl -s <http://podIP>**

 

**HANDS ON TIME**

*Check out the following screenshots*

 

SO, without even needing to setup fancy services we can simply do something like this:

![](003_Creating_Services_015.png)

 

*I essentially created 3 pods total.. One basic one and two running within a Deployment... Going into one of the ones in a cluster I used the command:*

**Kubectl get \[pod-name\] -o yaml**

*And at the very bottom I could see the IP address of the container running my application.... SO, by just exec shell into the one basic container... I was able to install curl and talk to the service running in the Pod in the deployment*

***Kubectl exec -it \[pod-name\] \-- sh***

***Apk add curl***

***Curl <http://10.1.0.34:80>***

*AND BOOM everything is already capable of talking to one another.... So what\'s up? WELL, what happens if the IP of this pod changes... meaning for some reason the Pod gets deleted the deployment creates a new Pod and now we have a new IP... would we be able to get our basic Pod communicating properly with the other one? PROBABLY NOT*

 

![](003_Creating_Services_016.png)

 

*This screen-shot is GOLD... EVERY WINDOW is showing something badass... this is NOT normal kubernetes work though... and more often than not we will NOT be doing things like this... but if we ever wanted to debug the communication happening across Pods... this would be a lot of fun.*

 

**NodePort Service**

![Terminal Help ! basic-pod.yml ! basic-deployment.yml node-port-service.yml - Kubern node-port-service.yml X Welcome to nginx! node-port-serv\'ice.yml \> {} spec \> \[ Services \> ! ! basic-serviceyml \] ports \> { } O \> \# nodePort 1 2 3 4 5 6 7 8 9 10 11 12 13 14 io.k8s.api.core.v1 .Serv•ice (VI \@service.json) apiVersion: VI kind: Service metadata name: myapp spec : type: NodePort selector : app: myapp ports : port: 80 targetPort: 80 nodePort: 30001 localhost :30001 Welcome to nginx! If you see this page, the nginx web server is successfully installed and working. Further configuration is required. For online documentation and support please refer to nginx.org. Commercial support is available at nginx.com. Thank you for using nginx. PROBLEMS OUTPUT TERMINAL DEBUG CONSOLE PS E: k apply -f .\\node-port-service.yml service/myapp created PS E: k get all pod / ba s ic - d eployment - name- 55dccd476f-6kb24 pod / basic -d eployment-name- 55dccd476f-jb27n READY 1/1 1/1 1/1 STATUS Running Running Running pod/basic-pod service/kubernetes service/myapp TYPE ClusterIP NodePort RESTARTS PORT(S) 443/TCP AGE 8m21s 14m 32h CLUSTER-IP 10.96.ø.1 10.98.66.169 READY EXTERNAL-IP \<none\> \<none\> UP-TO-DATE 2 DESIRED 2 80: 3øøø1/TCP 30s AVAILABLE AGE deployment . apps / basic -deployment -name 2/2 2 CURRENT 2 READY 2 AGE 8m21s replicaset . apps/ basic-deployment-name-55dccd476f PS E: ](003_Creating_Services_017.png)

 

*Essentially doing the exact same thing as our port-forwarding we had run directly using kubectl.*

 

**Load Balancer Service**

![i•rminal Help ! basic-pod.yml load-balancer-service.yml - Kube Welcome to nginx! ! basic-deployment.yml ! basic-serviceyml \] ports node-port-service.yml load-bala Services \> ! load-balancer-sewice.yml \> { } spec \> \[ 1 2 3 4 5 6 7 8 9 10 11 12 13 io.k8s.api.core.v1 .Serv•ice (VI \@service.json) apiVersion: VI kind: Service metadata name: myapp spec LoadBa1ancer type : selector : app: myapp localhost Welcome to nginx! If you see this page, the nginx web server is successfully installed and working. Further configuration is required. For online documentation and support please refer to nginx.org. Commercial support is available at nginx.com. Thank you for using nginx. ports : name port 80 targetPort : 80 PROBLEMS OUTPUT TERMINAL DEBUG CONSOLE PS E: k READY basic -deployment -name-55dccd476f-6kb24 1/1 basic -deployment -name-55dccd476f-jb27n 1/1 od PS E: k service/myapp created PS E: k get pods STATUS Running Running apply \_ f get all -show-labels RESTARTS AGE LABELS app=myapp , pod -templa t app---my app , pod -templa t . \\node-port-service. yml READY STATUS RESTARTS AGE PS E: k apply -f .\\load-balancer-service.yml service/myapp created PS E: ](003_Creating_Services_018.png)

 

*Boom we can now access our application from the browser...what this does is a BIT of magic....*

![PS C: WIE kubernetes k get services TYPE AGE ClusteriP CLUSTER-IP le.%.e.l EXTERNAL-IP PORT(S) 443/TCP 80 : 30865 nginx-loadbalancer LoadBalancer 10. løe. 187.151 localhost TCP 22s PS C: \\Users\\dwah1\\Dropbox\\Projects\\GitHub\\Courses\\DockerKubernetesCourseCod e\\samples\\services\> ](003_Creating_Services_019.png)

 

*It does a LoadBalancer but it ALSO creates a localhost loop-back address so we can just get to it... great for development... other services behind the scenes can call into our service.*

 

 

![Summary Pods live and die so their IP address can change Services abstract Pod IP addresses from consumers Labels associate a Service with a Pod Service types: ClusterlP (internal to cluster - default) NodePort (exposes Service on each\'s Node\'s LoadBalancer (exposes a Service externally) ExternalName (proxies to an external service) ](003_Creating_Services_020.png)

 

*There is ton to go still... but this is a great entry point to learn about how services stablish our networking strategy when using Kubernetes.*
