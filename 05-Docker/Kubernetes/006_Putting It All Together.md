Putting It All Together

Tuesday, April 20, 2021

5:44 PM

 

*Mostly watching this one... pretty awesome... one quick think I didn\'t write about earlier being LOGS*

 

![\# View the logs for a Pod\'s container kubectl logs \[pod- name\] \# View the logs for a specific container within a pod kubectl logs \[pod-name\] -c \[container-name\] \# View the logs for a previously running Pod kubectl logs -p \[pod-name\] \# Stream a Pod\'s logs kubectl logs -f \[pod-name\] ](006_Putting_It_All_Together_000.png){width="6.466666666666667in" height="2.7583333333333333in"}

 

*Also... harness the power of Describes:*

 

![\# Describe a Pod kubectl describe pod \[pod-name\] \# Change a Pod\'s output format kubectl get pod \[pod-name\] -o yaml \# Change a Deployment\'s output format kubectl get deployment \[deployment-name\] -o yaml ](006_Putting_It_All_Together_001.png){width="7.316666666666666in" height="2.475in"}

 

![\# Shell into a Pod container kubectl exec \[pod-name\] ---it sh ](006_Putting_It_All_Together_002.png){width="5.125in" height="1.0in"}

 

*WE CAN ALSO WATCH:\
* 

![Dans---MacBook---Pro:CodeWithDanDockerServices danwahlin\$ k + kubectl get pods NAME READY STATUS RESTARTS node-55f9b5cd69-khn4v 1/1 Terminating Dans---MacBook---Pro:CodeWithDanDockerServices danwahlin\$ k + kubectl get pods ------watch NAME READY node---55f9b5cd69---khn4v 1/1 node-55f9b5cd69-khn4v 0/1 node-55f9b5cd69-khn4v 0/1 node---55f9b5cd69---khn4v 0/1 STATUS Terminating Terminating Terminating Terminating : CodeWithDanDocke rServices RESTARTS danwahtin\$ get pods AGE 115s get pods ------watch AGE 2m2s 2m15s 2m25s 2m25s 1 c ](006_Putting_It_All_Together_003.png){width="8.958333333333334in" height="3.0833333333333335in"}

 
