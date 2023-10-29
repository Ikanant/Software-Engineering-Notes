Understanding Storage Options

Tuesday, April 20, 2021

3:50 PM

 

*Super common question that people in the training will most likely ask for... If a container goes down.... How can we handle having access to a certain file system?*

 

![Deployment ReplicaSet Container 8 Storage Pod Container Container ](004_Understanding_Storage_Options_000.png){width="7.625in" height="3.25in"}

 

 

Even without taking K8s into the conversation, if you asked anyone about how to properly store things when using docker containers they will most likely say: VOLUMES...

 

[A Volume can be used to hold data and state for Pods and containers.]{.underline}

 

-   Pods live and die. Their file system is SHORT-LIVED

-   Volumes can be used to store state/data and use it in a Pod

    -   We might be containerizing a DB for example.... Logs and data need to live elsewhere no?

-   A Pod can have multiple Volumes attached to it

-   Containers rely on a mountPath to access a Volume

-   Kubernetes supports

    -   Volumes

    -   PersistentVolumes

    -   PersistentVolumeClaims

    -   StorageClasses

 

 

**Volumes**

-   References a storage location

-   Must have a unique name

-   Attached to a Pod and may or may not be tied to the Pod\'s lifetime (depending on the Volume type)

-   A Volume Mount is used to reference a volume... It does this by name and defines a mountPath

-   Types

    -   emptyDir

        -   Empty directory for storing \"transient\" data (shares a Pod\'s lifetime) useful for sharing files between containers running in a Pod

        -   If Pod goes down, so does the volume

    -   hostPath

        -   Pod mounts nito the node\'s filesystem

        -   Easy to setup BUT if node goes down, you will loose data

        -   Ngs

            -   An NFS (Network File System) share mounted into the Pod

        -   configMap/secret

            -   Special types of volumes that provide a Pod with access to Kubernetes resources

        -   persistentVolumeClaim

            -   Provides Pods with a more persistent storage option that is abstracted from the details

        -   Cloud

            -   Cluster-wide storage

 

![Volume Types awsElasticBlockStore csi flocker local quobyte vsphereVolume azureDisk downwardAPl gcePersistentDisk rbd azureFile empty Dir glusterfs persistentVolumeClaim scalelO cephfs fc hostPath projected secret configMap flexVolume iscsi portworxVolume storageos ](004_Understanding_Storage_Options_001.png){width="7.408333333333333in" height="3.816666666666667in"}

>  

*It really comes down as the administrators to decide which type of volume we will end up using*

 

**EmptyDir Volume**

![apiVersion : kind: Pod spec : volumes : VI --- name: html emptyDir: containers : - name: nginx image: nginx : alpine volumemounts : - name: html mountPath: /usr/share/nginx/html readOn1y: true --- name: html-updater image: alpine command: \[\"/bin/sh\", \" c \] args : - while true; sleep 10; volumemounts : - name: html mountPath : do date done \'html \[html/ index. html ; Define initial Volume named \"html\" that is an empty directory (lifetime of the Pod) Reference \"html\" Volume and define a mountPath Update file in Volume mount /html path with latest date every 10 seconds Reference \"html\" Volume (defined above) and define a mountPath ](004_Understanding_Storage_Options_002.png){width="6.4in" height="3.4583333333333335in"}

 

**HostPath Volume**

![apiVersion : kind: Pod spec : volumes: VI --- name: docker-socket hostPath : path: /var/ run/docker. sock type: Socket containers : - name: docker image: docker command: \[ \" sleep\" \] args: \[\"100000\" \] volumeMounts : - name: docker-socket mountPath: /var/ run/docker. sock Define a socket volume on host that points to /var/run/docker.sock \< Reference \"docker-socket\" Volume and define mountPath ](004_Understanding_Storage_Options_003.png){width="6.175in" height="3.2916666666666665in"}

 

 

 

![Cloud Volumes Pod volume Container Cloud providers (Azure, AWS, GCP, etc.) support different types of Volumes: Azure - Azure Disk and Azure File AWS - Elastic Block Store GCP - GCE Persistent Disk ](004_Understanding_Storage_Options_004.png){width="7.091666666666667in" height="2.175in"}

**Azure:**

![apiVersion: kind: Pod metadata : name: my-pod spec : volumes : - name: data azureFi1e : secretName: cazure-secret\> shareName: ghare-name» readOn1y: false containers : - Image: somexmage name: my-app volumeMounts : - name: data mountPath: Define initial Volume named \"data\" that is Azure File storage Reference \"data\" Volume and define a mountPath /data/storage ](004_Understanding_Storage_Options_005.png){width="5.325in" height="2.6666666666666665in"}

**AWS:**

![apiVersion: kind: Pod metadata : name: my-pod spec : volumes : - name: data awsE1asticB10ckSto re : volumeID: «volume\_ fsType: ext4 containers : - Image: somexmage name: my-app volumeMounts : - name: data mountPath: /data/storage Define initial Volume named \"data\" that is a awsElasticBlockStore ](004_Understanding_Storage_Options_006.png){width="5.316666666666666in" height="2.5083333333333333in"}

**Gce\
** 

![apiVersion: kind: Pod metadata : name: my-pod spec : volumes : - name: data gcePe rsistentDisk : pdName: datastorage fsType: ext4 containers : - Image: somexmage name: my-app volumeMounts : - name: data mountPath : Define initial Volume named \"data\" that is a gcePersistentDisk Reference \"data\" Volume and define a mountPath /data/storage ](004_Understanding_Storage_Options_007.png){width="5.241666666666666in" height="2.466666666666667in"}

 

*Guess one question I have is, how do I know which Pod has a volume?* Just use DESCRIBE

![\# Describe Pod kubectl describe pod \[pod-name\] Vo lumes: html: Type: Medium: EmptyDir (a temporary directory that shares a pod\'s lifetime) \# Get Pod YAML kubectl get pod \[pod-name\] vo lumeMounts : - mountPath: /html name: html ---o yaml ](004_Understanding_Storage_Options_008.png){width="7.091666666666667in" height="3.783333333333333in"}

 

![](004_Understanding_Storage_Options_009.png){width="3.35in" height="0.9083333333333333in"}

 

**PersistentVolumes AND PersistentVolumeClaims**

 

**PersistentVolume:** [(PV) is a cluster-wide storage unit provisioned by an administrator with a lifecycle independent from a Pod.]{.underline}

*This could talk to cloud or local storage... In order to use one of these we essentially would use a PersistentVolumeClaim*

 

**PersistentVolumeClain:** [(PVC) is a request for a storage unit (PV)]{.underline}

 

-   A PersistentVolume is cluster-wide! It is a resource that relies on some type of network-attached storage (NAS)

-   Normally provisioned by a cluster administrator

-   Available to a Pod even if the Pod is rescheduled to a different Node

    -   No matter where our Pod is scheduled... we are going to be OK

-   Rely on a storage provider such as NFS, cloud storage or other options

-   Associated with a Pod by using a PersistentVolumeClaim (PVC)

 

![](004_Understanding_Storage_Options_010.png){width="2.0in" height="1.95in"}

 

![PVC Pod Container Storage kubernetes ](004_Understanding_Storage_Options_011.png){width="6.833333333333333in" height="2.2083333333333335in"}

 

 

**PV YAML**

*People often complain about PV due to the complexity of the YAML file... or at least how specific we need to be to get it running properly... for this I just encourage people to look in the online examples on github.*

 

![](004_Understanding_Storage_Options_012.png){width="4.791666666666667in" height="2.375in"}

 

*Checkout:* <https://github.com/kubernetes/examples>

 

 

![apiVersion: VI kind: PersistentV01ume metadata : name: my-pv spec: capacity: IOGi accessModes : - ReadWriteOnce - ReadOn1yMany persistentV01umeRe1aimP01icy : azureFiIe : secretName: \<azure-secret\> shareName: \<name_from_azure\> readOn1y: false Retain Create PersistentVolume kind Define storage capacity One client can mount for read/write Many clients can mount for reading Retain even after claim is deleted (not erased/deleted) Reference storage to use (specific to Cloud provider, NFS setup, etc.) ](004_Understanding_Storage_Options_013.png){width="6.825in" height="3.35in"}

*This is using Azure... but plenty of other examples out there for other options.*

 

**PVC YAML**

![](004_Understanding_Storage_Options_014.png){width="7.375in" height="3.783333333333333in"}

 

 

![kind: PersistentV01umeC1aim apiVersion: VI metadata : name: pv-dd-account-hdd-5g annotations : volume. beta.kubernetes.io/storage-class: accounthdd spec : accessModes : - ReadWriteOnce resources : requests : storage : 5Gi Define a PersistentVoIume( Define access mode Request storage amount ](004_Understanding_Storage_Options_015.png){width="5.85in" height="2.6666666666666665in"}

*Define an ACCESS MODE here means hooked up to a SINGLE Pod that will be able to Read/Write to the storage.*

*Here we determine we need 5Gbs of storage, but recall the PV had 10Gb max*

 

**Pod YAML**

 

![PVC pod Container ](004_Understanding_Storage_Options_016.png){width="5.816666666666666in" height="2.7916666666666665in"}

 

![kind: Pod apiVersion: VI metadata : name: pod-uses-account-hdd-5g labels : name: storage spec : containe rs : - image: nginx name: az-c-el command : - /bin/sh - while true; do echo \$(date) /mnt/blobdisk/outfile; sleep volumes : - name: blobdisk01 persistentV01umeC1aim: claimName: pv-dd-account-hdd-5g done Create Volume that binds to PersistentVolumeClaim ](004_Understanding_Storage_Options_017.png){width="6.566666666666666in" height="3.8666666666666667in"}

*Very similar to what we have done in the other Volumes examples, except we are setting it as a persistentVolumeClaim with the name we provided the PVC from the screenshot above.*

 

![volumeM0unts : - name: blobdiskØ1 mountPath: /mnt/blobdisk ](004_Understanding_Storage_Options_018.png){width="3.225in" height="1.0583333333333333in"}

 

![command : - /bin/sh --- while true; do echo S(date) /mnt/blobdisk/outfile; sleep 1 ; done ](004_Understanding_Storage_Options_019.png){width="4.366666666666666in" height="1.3916666666666666in"}

 

*SUMMARY:*

![kind: Pod apiVersion: VI metadata : name: pod-uses-account-hdd-5g labels : name: storage spec : containe rs : - image: nginx name: az-c-el command : - /bin/sh --- while true; do echo S(date) /mnt/blobdisk/outfile; sleep volumeM0unts : - name: blobdiskØ1 mountPath: /mnt/blobdisk volumes : - name: blobdisk01 persistentV01umeC1aim: claimName: pv-dd-account-hdd-5g done Mount to Volume Create Volume that binds to PersistentVolumeClaim ](004_Understanding_Storage_Options_020.png){width="7.35in" height="4.316666666666666in"}

 

*There is one little piece we are missing... and that is a StorageClass*

 

**StorageClasses**

*While it is straight forward to create a set of PV and PVC resources... there is something else we can use called StorageClasses*

 

***StorageClass:*** [A StorageClass is a type of storage template that can be used to dynamically provision storage.]{.underline}

 

*Similar as before... StorageClasses can certainly be setup locally... BUT in the real world, an administrator of some kind usually manages these resources*

 

![III ı ](004_Understanding_Storage_Options_021.png){width="4.783333333333333in" height="3.658333333333333in"}

*So what\'s up with the SC:*

-   Used to define different \"classes: of storage

-   Act as a type of storage template

-   Supports dynamic provisioning of PersistentVolumes

    -   *What DYNAMIC provisioning would allow us to do... is for an admin to setup storageClass... THEN we can request through a PVC (a claim)... and then it can Dynamically setup the PV...*

    -   *This is awesome since now us a developers, do not need to bother admins with requests to setup YET ANOTHER PV for us*

-   *Administrators don\'t have to create PVs in advance*

 

 

![ιιι ι ](004_Understanding_Storage_Options_022.png){width="6.308333333333334in" height="2.6666666666666665in"}

 

 

![apiVersion: storage.k8s.io/vI kind: StorageCIass metadata : name: local-storage reclaimPoIicy: Retain provisioner: kubernetes. io/no-provisioner volumeBindingMode: WaitForFirstConsumer API version A StorageCIass resource Retain storage or delete (default) after PVC is released Provisioner (volume plugin) that will be used to create PersistentVoIume resource Wait to create until Pod making PVC is created. Default is Immediate (create once PVC is created) ](004_Understanding_Storage_Options_023.png){width="6.908333333333333in" height="3.225in"}

*Notice how we currently have the provisioner to have \*no provisioner... Essentially this is where we would choose depending of the type of storage we would need. At this point we would have too research and look at the docs.*

 

![apiVersion: VI kind: PersistentV01ume metadata : name: my-pv spec : capacity : storage: 1BGi volumeMode: Block accessModes : - ReadWriteOnce storageC1assName: local-storage local : path: /data/storage nodeAffinity : required : nodeSe1ecto r Te rms : - matchExpressions: - key: kubernetes . io/hostname operator: In values : - cnode-name\> One client can mount for read/write Reference StorageClass Path where data is stored on Node Select the Node where the local storage PV is created ](004_Understanding_Storage_Options_024.png){width="6.483333333333333in" height="3.2916666666666665in"}

 

![apiVersion: VI Define a PersistentVolumeClaim (PVC) kind: PersistentVoIumeCIaim metadata : name: my-pvc spec : accessModes : - ReadWriteOnce storageCIassName : resources : requests : storage : Access Mode and storage classification PV needs to support local-storage \< Storage request information ](004_Understanding_Storage_Options_025.png){width="6.525in" height="2.5833333333333335in"}

 

![apiVersion: apps/vl kind: \[Pod I Statefu1Set I Deployment\] spec : volumes : Define a Volume - name: my-volume Use a PVC to claim the required persistentV01umeC1aim: storage claimName: my-pvc ](004_Understanding_Storage_Options_026.png){width="6.25in" height="2.466666666666667in"}

 

*I am going to skip noting and screenshotting the example. I will come back to it if necessary*

<https://app.pluralsight.com/course-player?clipId=25fd5b96-564e-4c09-ad98-41191d72e332>
