

# ................... 287 Kubernetes Interview Questions  ....................

## By  Mamun Rashid :: https://www.linkedin.com/in/mamunrashid/ 

### Last Updated: 2022.12.13

##

#### 1. So, what have you done with Kubernetes? This question comes up all the time!

#####   Answer: 

#####     While this seems easy, a prepared and practiced answer is significantly better than an impromptu one.

#####     You answer would be uniqe to your experience, but, here are some possibilities.


######     a. created clusters
######     b. upgarde master and nodepool versions
######     c. upgraded legacy monitoring 
######     d. added Istio (Kiali)
######     e. added weave
######     f. deployed via helm charts
######     h. healthcheck scripts for various workloads
######     g. deployed spinnaker 
######     h. configured HPA
######     i. day to day: configmps, secrets, PVs, PVCs
######     j. troubleshot operational issues
######     k. stateful sets 
######     l. created CSRs and signed certificates


## ........

#### 2. You have 2 different contexts (A and B). Context A has a secret named foo. Context B does not. What would be a quick way to create the same exact secret in Context B?

     Answer: 
       1. Switch to Context A
       2. kubetcl get secret foo -o yaml > foo.yaml
       3. Switch to Context B
       4. kubectl apply -f foo.yaml

## .



## ......

#### 3.  There are more than one way to implement Ingress? What did you use to implement Ingress?

    Answer:  So, ingress is IMPLEMENTED by Ingress Controllers. There are at least 12.
             Most common is a Load Balancer (GCP/AWS). 
             Another popular one is Nginx Ingress Controller.
             See below for a longer list. (Question #8)

## .



## ......

#### 4. Why do we need Kubernetes? What problems does it solve?

     Answer: As soon as we decide to use docker/container as platform, we run into new issues such as:
              a. orchestration
              b. inter-container communication
              c. autoscaling
              d. observibility
              e. security
              f. persistent and/or shared volumes
              and more

              Kubernetes solves these problems.


## .


## .....

#### 5. What is the difference between Ingress and Ingress Controller:

    Answer: Ingress Controller FULFILLS ingress requirements
            Defining and ingress has no actual impact on traffic.
            Traffic is only acted upon once you have created an Ingress Controller (e.g. Load Balancer or Nginx Ingress Controller)

## .


## .....

#### 6. Most common type of Ingress Controller?

    Answer: Load Balancers

## .


## .....

#### 7. Kubernetes as a project supports and maintains which 3 Ingress Controllers?

    Answer: AWS, GCE, and nginx ingress controllers.
            (This is straight from Kubernetes documentation)

## .


## .....

#### 8. Besides those 3, what other ingress controllers are there?

    Answer:  From:  https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/

    a. HA Proxy
    b. Istio Ingress
    c. Traefik kubernetes Ingress Provider
    d. Skipper
    e. Voyager
    f. Tyk Operator
    g. Gloo (open source)
    h. AKS Application Gateway Ingress Controller (Azure)
    i. Ambassador (envoy-based)
    j. Enroute (another envoy-based Ingress Controller)
    (and more)

## .


## .,...

#### 9. How would one start up a Kubernetes cluster to deploy containers/pods on (in GCP)?

     Answer: 
       a. via GCP GUI  OR
       b. via GCP cloud shell window OR
       c. gcloud CLI
       d. Terraform
       e. Google Deployment Manager
       

## .



## ......

#### 10.   If a container keeps crashing, how do you troubleshoot?

    Answer: You can use --previous option with logs command to see the logs of a crashed container.
      (kubectl logs --previous)

## .


## ......

#### 11.  What happens to containers if they use too much cpu or memory?

    Answer: if they use too much memory, they are evicted.
            if they use too much cpu, they are throttled.

## .


## ......

#### 12.  How do you manage scaling in Kubernetes?

    Answer: 
      This artcile answers it very well:
      https://www.replex.io/blog/kubernetes-in-production-best-practices-for-cluster-autoscaler-hpa-and-vpa

      a. hpa for pods (horizontal pod autoscaler)
      b. vpa for pods (vertical pod autoscaler)
      c. Cluster Autoscaler:
           The cluster autoscaler is a Kubernetes tool that increases or decreases the size of a Kubernetes cluster (by adding or removing nodes), based on the presence of pending pods and node utilization metrics

## .



## ......

#### 13. How have you used RBAC with Kubernetes ?

    Answer: Answer will depend on your use case. One possible answer is to have Service accounts that do certain things within the cluster.
            By the way, RBAC in Kubernetes is just AWS IAM Policies and Bindings. In RBAC, you have subjects (who gets the permission), verbs (what can the subject actually do), and rolebinding (subject linking to roles) and roles.


## .


## ......

#### 14. If you have 200 micro-services in your clusters, how do you manage security of each one? How do you avoid toil?

    Answer: RBAC is the answer. You define roles. And you place subjects in those roles. Each role then will have access to X Y Z etc. This is really no different than AWS or AD.

## .


## ......

#### 15. Tell me about the hardest production Kubernetes issue you solved or faced?

    Answer: 

      Your answer will be unique to your experience. But, here is a hypothetical answer.

      There are N micro-services. One of them gets a new version. But, the HPA for those pods are set wrong. Container keep crashing. This causes cascading failures for many other micro-services. 
      Solution: Fix the HPA settings and add circuit-breakers in the consuming micro-services.

## .


## ......

#### 16. You want to know how to make yaml files for making PODs and you have no access to internet. What do you do?

    Answer: kubectl explain pod --recursive

      It will show you all fields in a mapped kind of fromat so you exacly what field go where

      Simillarly: kubectl explain pv --recursive    (for PVs)

## .

## ......

#### 17. How can you have SSL certificates in Kubernetes?

    Answer: SSL cert can be a secret. Then that secret can be mounted on a pod and that pod can whatever it wants with it (e.g. host a SSL web site)

## .


## ......

#### 18. Opensource Tool to switch contexts easily:

    Answer: kubectx

## .


## ......

#### 19. Opensource menu-driven text-based flexible Tool to manage Kubernetes everything:

    Answer: k9s

## .


## ......

#### 20. "kubectl explain" command is great, but you must know the exact name of the resource (e.g. pod/services/persistentvolume) to get the details, unless you do recursive. How do you get the names of these resources from command line?

    Answer: kubectl api-resources  (gives you a list and shortnames and more)  

## .

## ......

#### 21. Name some of the other verbs that kubectl has besides "run" "create" or "apply" ?

         Answer: There are many! Some examples below:

         expose, set , explain, get, edit, delete, rollout, scale, autoscale
         certificate, cluster-info, top, cordon, uncordon, drain, taint
         describe, logs, attach, exec, port-forward, proxy, cp, auth, debug
         diff, apply, patch, replace, wait, kustomize, label, annotate,
         completion, api-resources, api-versions, config, plugin, version

        Some of more frequently used ones are: logs, get, port-forward and label.

## .




## ......

#### 22. What might you get when you run kubectl api-resources? 

    Answer: api-resources is fancy term. Basically you get stuff like pods/secrets/config-maps all that stuff.

## .



## ......

##### 23. How else can you get help with kubectl? (besides kubectl explain command)

    Answer: kubectl --help  is actaully better than kubectl explain in my opinion.

## .




## ......

#### 24. You ran "kubectl --help" , but you want a little more help. What to do?


    Answer:
       kubectl get --help 
       kubectl top --help 
       kubectl describe --help 

## .




## ......

#### 25. Outline the steps to deploy additional scheduler on a Kubernetes cluster (not GKE)

     Answer:
       Package the new scheduler in a docker image
       Put that image in a registry
       Create a deploymentment file with type: deployment and component: scheduler (in namespace kube-system)
       Deploy the the scheduler with apply -f scheduler.yaml command

## .



## ......

#### 26. List out 2 use cases for Daemonsets and explain why it is more appropriate to use daemonset than deployment for those use case:

     Answer:
       1. Pod that collects logs. Better to use daemonsets for this because you can logs to be fed from all pods (e.g. to kibana). Otherwise you have to make this part of EVERY deployment which would be annoying and repetitive.
       2. Pod that runs monitoring (e.g. dynatrace or datadog). Reason is the same as above.

## .



## ......

#### 27. How to move workload to new nodepool? 

    Answer: cordon and drain
        1. cordon means: dont add any more pods to this nodepool
        2. drain means: move current pods out of it

## .  


## ......

#### 28. Is ClusterIP private or public?

    Ans: Private

## .

## ......

#### 29. Which one will allow to access your services from internet: cluster ip or nodeport? 

    Answer:  nodeport. confirmed!  
             why? Because NODE is a VM with an external IP and thus can be reached.
             Cluster IP is 10.x IP (internal)

## .

## ......

#### 30. For a service, when we use nodeport, EVERY node does what?

    Answer: Gives that service an IP and proxy's it. confirmed 

## .


## ......

#### 31. What does it mean when we say that a node proxy's a service?

    Answer: The node forwards the traffic to a pod that is part of the service.

## .


## ......

#### 32. 2 ways to let container have access to a secret: 

   Answer: Volume and ENV variable

## .


## ......

#### 33. How can a container have access to secret via ENV variable? 

    Answer: You can define a ENV in yaml file just like everyhing else and container can just do echo $WHATEVER

## .

## ......

### 34. One-liner kubectl commad to run a pod with nginx:alpine 

    Answer:  k run nginx-pod --image=nginx:alpine 

             (nginx-pod is arbitrary pod name)

## .

## ......

#### 35. One liner command to  run a pod with a label  

    Answer: kubectl run foobar --image=redis:alpine -l label1:foo 

## .


## ......

#### 36. kubectl command to show labels of all pods in default namespace:  

    Answer: kubectl get pods --show-labels 

## .

## ......

#### 37. Whenever you run a kubectl command, it runs in the the default namespace. How do you make in run in a different namespace?

    Answer: use -n namespace_name   (to whatever kubectl command you are running.)

## .

## ......

#### 38. Command to create a namespace: 

    Answer: kubectl create ns foobar # create a namespace

## .

## ......

#### 39. When using kubectl command, how do you to get output in json format?  

    Answer: kubectl get nodes -o json # json format

## .


## ......

#### 40. kubectl expose command: port VS targetport:  (which one is which ?)

    Answer:
       port : on the cluster
       targetport: on the container (just like ALB)

## .




## ......

#### 41. Command to expose a pod as a service 

    Answer: kubectl expose pod foobarpod --name foobarservice --port 6379 --target-port 6379  # expose a pod as a service
            (NOTE servicename is specified: foobarservice)

## .



## ......

#### 42.  Command to get details of a service : 

     Answer: kubectl describe svc foobarservice # get details of that service

## .



## ......

#### 43. Command to create a deployment from image: foobar/webapp-color 

    Answer: kubectl create deployment foobardeployment --image=foobar/webapp-color 

## .



## ......

#### 44. Command to scale deploayment named foobardeployment to 2 replicas  

    Answer: kubectl scale deployment foobardeployment --replicas=2 # scale that to 2 replicas  

## .



## ......


#### 45. Can you scale a kubernetes service?

    Answer: No. You can scale deployments and replicasets

## .


## ......

#### 46. If you want your kubernetes command to have a scope of ALL namespaces, how do you do that?

    Answer: add -A to the command

## .




## ......

#### 47. Are environment variables encrypted in Kubernetes? 

    Answer: No
 
## .




## ......

#### 48. By default, can a pod in one namespace talk to another pod in another namespace? 

    Answer: Yes.

## .



## ......

#### 49. How to generate a yaml file from an imperative command you know works ? 

    Answer: add: --dry-run=client -o yaml 

## .




## ......

##### 50. Write a kubectl command to Create a static pod, have it run a command (so it does not exit). dryrun so that you get yaml file saved : 

    Answer: kubectl run static-busybox --image=busybox --command sleep 1000 --dry-run=client -o yaml > static-pod-busybox.yaml

## .



## ......

#### 51. By default, where does yaml files for static POD files go:  

    Answer: /etc/kubernetes/manifests/  (on the node)

## .




## ......

#### 52. What is a static pod?

    Answer: This is from official documentation.  Static Pods are managed directly by the kubelet daemon on a specific node, without the API server observing them.

## .


## ......

#### 53. Kubectl command to take all the details for a.yaml file and create the resource it tells API to crate: 

    Answer: kubectl apply -f a.yaml  

## .



## ......

#### 54. Kubectl command to list all the pods in foo namespace: 

    Answer: kubectl get pods -n foo

## .



## ......

#### 55. There is pod named foo. it is in crashloopbackoff state. How to find the cause using a kubectl command? 

    Answer: kubectl describe pod foo

    # to see why it is in crashlookpbackoff state

    What you might see is for example, container's "command" has a mispelling in it. (Just an example)

## .



## ......

#### 56. Scenario Question: You have a container that keeps crashing because its "command" section has a misspelling. How do you fix this?

    Answer:
      1. generate the yaml file, 
      2. fix it, 
      3. kill the pod, 
      4. re-run with the correct yaml file (kubectl apply -f)

## .



## .......

#### 57. How to get a yaml file out of running/crashing pod? 

    Answer: kubectl get pod foo -o yaml > foo.yaml 

## .



## .......

#### 58. How to terminate a running pod? 

    Answer: kubectl delete pod foo

## .



## ......

#### 59. Command to see a list of running pods in the default namespace: 

    Answer: kubectl get pods 

## .



## ......

#### 60. Kubectl command to make a new yaml file for a service by exposing a already running deployment that runs a pod.  Name of the deployment: foo.

    Answer: Kubectl expose deployment foo --name foo-service --type=NodePort --port 8080 --target-port=8080 --dry-run=client -o yaml > svc.yaml

## .



## ......

#### 61. jsonpath example of getting "everything"  (about nodes)  .  This is not really an interview question. But, its goog to know this in case JSON PATH topic comes up.

    Answer: kubetcl get nodes -o jsonpath='{.items[*]}'   # everything, so tons of data
            * Thing to remember is syntax starts out like awk (single quote and swiggly bracket and then follows dots for JSON levels and [] for lists.

## .



## ......

#### 62. jsonpath example of getting just the level "status" for all nodes 

    Answer: kubectl get nodes -o jsonpath='{.items[*].status}'   # quite a bit of data comes back

## .



## ......

#### 63. jsonpath comamnd to get only status.nodeInfo of each node . This is not really an interview question. But, its goog to know this in case JSON PATH topic comes up.

    Answer: kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo}'   # better, more managable amount of data

## .



## .......

#### 64:  Your computer has no access to internet. Which kubectl command  can you use to find out syntax of making a pv.yaml : 

     Answer: kubectl explain pv --recursive  # to find out syntax of making a pv.yaml

## .


## ......

#### 65. What is the different between PV and PVC?

    Answer: PV is basically a disk volume of some sort.  PVC is a link between that volume and a pod.

## .



## ......

#### 66. Kubectl command to get a list of PVs

    Answer: kubectl get pv   

## .


## ......

#### 67. Kubectl command to get detail about a PV   

    Answer: kubectl describe pv foo  

## .


## .......

#### 68. How does the Master server talk to etcd ?

     Answer: It makes a call etcd (runs on localhost in most cases). To do that, it authorizes itself with etcd using 2 certs and 1 key.
               AND sends commands to etcd.
             On the master node, the file that has these configs is at : /etc/kubernetes/manifests/etcd.yaml
             That file in turn , points to the 2 cert files and 1 key file.

## .



## .......

#### 69. Some example of commands the master server can send to etcd (once authenticated with certs and key):

     Answer:
       member list
       snapshot save /tmp/etcd-backup.db
       snapshot status /tmp/etcd-backup.db -w table

## .


## .......

#### 70. Steps to create a pod called foo with image redis with CPU Request set to 2 CPU and Request as 400MiB


       Answer:
         a. first create a yaml file: (dry-run command)
            kubectl run foo --image=redis --dry-run=client -o yaml > foo.yaml
         b. edit the yaml file:
            in the resources section of "spec" section:
            cpu: 2
            memory: 400MiB
         c. kubectl apply -f ./foo.yaml

## .



## ......

#### 71. True or False: POD DEFINITION (yaml) ONLY points to PVC (claim), it does not refer to the PV anywhere. 

     Answer: True

## .


## .......

#### 72. Kubectl command to create deployment with busybox version 1.13  
     
     Answer: kubectl run foo-deploy --image=busybox:1:13 --replica=1 --record  # create deployment w busybox 1.13

## .


## ......

#### 73. kubectl command to look at deployment's history: 
   
     Answer: kubectl rollout history deployment foo-deploy # look at deployment's history  

## .


## ......

#### 74. kubectl command to change the image version of a deployment on the fly:  

     Answer:  kubectl set image deployment/foo-deploy busybox:latest --record # CHANGE THE IMAGE VERSION

## .


## ......

#### 75. Kubectl command to a list of existing deploymnets 

    Answer: kubectl get deployments    

## .



## ......

#### 76. Why do you need certificates in Kubernetes, anyway?

     Answer: For one thing, the API server won't talk to you , if you don't have a signed client certificate. So, any client who wants to do ANYTHING with the API server (e.g. even kubectl) better have a signed certificate!

     Please read:  https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/

## .


## ......

#### 77. Why are .csr files have CSR extension? What is CSR all about?

     Answer: CSR = Certificate Signing Request.  
             For example A needs B to give A a signed certificate SO THAT A can later talk to B using that certificate. 
             A will send a CSR (Certificate Signing Request) to B. The file that A sends to be will be CSR and thus will have .csr extension.

             Please read:  https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/

## .



## ......

#### 78. Why does Kubernetes have certificate API ?

     Answer: So that the certificate signing process can be automated end to end.

## .


## ......

#### 79. What's an easy way lookup kubernetes documenation on the fly simply using kubectl command?

     Answer: kubectl explain   

## .


## ......

#### 80. Kubernetes Security: How are some of the ways you can protect your container images?

     Answer:
       a. Update them (to get latest security patches at the OS level)
       b. Scan them regularly
       c. Sign them digitally

## .



## ......

#### 81. Can you think of some general areas of Kubernetes where you would want to think about security:

     Answer:
       a. Your container images
       b. Your container registry
       c. Your kubernetes run time infrastructure (e.g. etcd)
       d. Hosts (where Kubernetes nodes are running)
       e. Kubernetes Secrets
       f. Kubernetes Certificates
       g. RBAC entities

## .



## ......

#### 82. Processes within a container: How to they (security-wise) talk to API server running on the master node?

     Answer: Using a Kubernetes Service Account

## .


## ......

#### 83. What does base64 command do?

     Answer: it "encodes" a file or strings.

     Note: The reason why this is related to Kubernetes is that sometimes you use this command to encode soemthing before putting it in the yaml file.

## .


## ......


#### 84. How do you generate a CSR within the Kubernetes system?

     Answer: 
       a. create a .csr file
       b. encode it
       c. create a yaml file (Kind: CertificateSigningRequest) using the encoded CSR
       d. kubectl apply -f CertificateSigningRequest.yaml

## .


## ......

#### 85. If you have created CertificateSigningRequest, but you have not approved it yet, what status do you get if you run "kubectl get csr" command?  

     Answer: You will see that the request is in "pending state"

## .


## .......

#### 86. Command to approve a CSR? 

     Answer: kubectl certificate approve foo-csr   
      
       Example output:  certificatesigningrequest.certificate.k8s.io/foo-csr approved

## .


## ......

#### 87. Kubectl command to create role:

     Answer:  kubetcl create role

       A detailed example: kubectl create role foo --resource=pods --verb=create,list,get,update,delete --namespace=development
                           role.rbac.authorization.k8s.io/foo created

## .



## ......


#### 88. Command to describe a role: 

     Answer: kubectl describe role foo -n foo_namespace  

## .


## ......

#### 89. Why is important to keep etcd secure and encrypted?

     Answer: etcd data store all your Kubernetes data including Kubernetes secrets

## .


## ......

#### 90. Which component of Kubernetes has to have "certificate authority" ?

     Answer: Master Node  (because clients will authenticate with the API server using client certificates)

## .


## .......

#### 91. 3 Steps for creating a CA (Certificate Authority) on master node?

    Answer: (On a managed Kubernetes like GKE and EKS, you don't need to do this):
      a. create a private key
      b. create CSR
      c. self-sign the CSR

## .



## .......

#### 92. Can you run etcd over HTTP?

  Answer: Yes, but horrible idea, basically all traffic do and from etcd will not be encrypted

## .


## .......

### 93. Command to insert and Key-Value (foo=bar) pair into etcd?

  Answet: etcdctl put foo "bar"

## .


## ......

#### 94. When you tell Kubernetes to run a pod, who decides which node gets that pod?

  Answer: Scheduler

## .


## ......

#### 95. What if you don't like the default scheduler that comes with Kubernetes?

  Answer: You can always run your own schdeluer

## .


## .......

#### 96. If a node has taint, what you have to do to your pod, for it to be able to run on that node?

  Answer: You have to give the pod the same toleration

## .


## ......

#### 97. If you want a pod to run on specific node, which feature do you have to use?

  Answer: Node Affinity

## .


## ......

#### 98. If we already have a liveness probe, why do we need a readiness probe?

  Answer: There are times, when a container fails liveness probe and yet we do not want to container to be killed. For example, if a container takes time to ready (loads large data set). In this case, liveness probe would fail and (without a readiness probe), Kubernetes would kill the container. A readiness probe tell Kubernetes to wait for the container finish doing all its prep work.

## .


## ......

#### 99. What does it mean for Kubernetes to drop support for Docker?

  Answer: Best answer is given here:  https://kubernetes.io/blog/2020/12/02/dont-panic-kubernetes-and-docker/ . Summary is that, you would have switch to other run time (e.g. containerd or CRI-O) by the time Kubernetes 1.22 comes around. 

## .


## .......

#### 100. What is "logging driver" ?

  Answer: Docker has the ability to send logs to various places (e.g. awslogs or fluent and many more). Each one of these is a logging driver.

## .


## ......

#### 101. Which component collects and aggregates the metrics ?

  Answer: cAdvisor (which is part of kubelet on worker nodes)
          Those are then sent to Metric Server (running on master nodes). 
          Metrics Server exposes them via kube-api (also running on the master node)

## .


## .......

#### 102. When you run "kubetcl top", which component are you talking to?

     Answer: kube-api (which gets its data from metric server)

## .


## ......

#### 103. By default, conatiner runs with with what UID?

     Answer: 0  (i.e. root).  This can be potentially bad, in case container is somehow able to get a hold of the host OS.

## .



## .......

#### 104. What is the idea behind "Security Context" ?

     Answer: Security Context is what level of permissions we give the container as it runs. BY default, it runs with UID 0, which is potentially bad. Be using runAsUser, runAsGroup and fsGroup, 
       we can limit what can the container do on the host. This is "Security Context"

## .


## .......

#### 105. What is "Ambassador Pattern" ?

     Answer: When the sidecar proxy's the connections from the main container to the outside world.

## .


## .......

#### 106. What is "Adapter Pattern" ?

     Answer: When the sidecar re-formats the output of the application running on the main container to another desired format.
               This way, you don't have to re-write the application code when there is need to re-format the output for some other system to consume.

## .


## ......

#### 107. Can you describe a use-case where the ambassador pattern can be of use?

     Answer: If you have legacy application which cannot be modified, BUT you have a need to change to the port on which this app needs to listen on, the ambassador container can listen on the new port and pass on the traffic to the old port which did not get modified.

## .


## .......

#### 108. What is the difference between a label and selector?

     Answer: Labels are basically tags. Selectors use key-value pairs to pick out objects (e.g. pods) to work on.

## .



## ......

#### 109. What is a network policy in Kubernetes?

     Answer: A network policy is equivalent to a Security Group in AWS. You define who can talk to who via network policy.

## .


## .......

#### 110. Network Policies often rely on what?

    Answer: labels and selectors

## .


## ......

#### 111. When do maxSurge and maxUnavailable come in to play?

    Answer: In Rolling Updates of Deployments.
            maxSurge tells Kubernetes how many (or percent) extra pods it can create during rolling update.
            mxUnavailable tells Kubernetes how many (or percent) pods can be unavailable during the rolling uodate.

## .


## ......

#### 112. Why do we need HPA when we already have maxSurge and maxUnavailable?

    Answer: HPA is an autoscaling thing. maxSurge and maxUnavailable only apply during rolling updates.

## .



## ......

#### 113. Difference between Service Port and Target Port?

     Answer: Service Port is where users come to get the micro-service. Target Port is the port of the container/pod where the application listens and exposes. 

## .


## ......

#### 114. You are configuring a service and you have made a mistake with labels and/or selectors. How does this manifest itself often?

     Answer: You will see the service and there will be no endpoint.

## .


## ......

#### 115. You are logged in to conext via kubectl on your Mac. How can you see if you have permission to update pods? 

       Answer: kubectl auth can-i update pods   
               (You get back: yes)

## .



## ......

#### 116. Let's say you manage 100 GKE Clusters. You want to run a kubectl command. How do you make sure your command will be executed on the right cluster?

     Answer: You will have 100 contexts (one for each cluster you have logged in to). You must switch to to the right context before running the command.  There is a open-source CLI tool called kubectx that helps you with this.

## .


## ......

#### 117. What is a super quick way to create a service?

     Answer: Using a kubectl expose command

        Example: kubectl expose pod foopod --name=fooservice --port=80 --target-port=80 --type=ClusterIP
                 :: service/ngnix-resolver-service exposed

## .



## ......

#### 118. How does Kubernetes do DNS interally?

       Ans: kube-system namespace has pod(pods) that DNS servers.
            You can see them by running: kubectl get po -A | grep dns

## .


## .......

#### 119. If you are on a node, how do you look for running container? 

     Answer:  docker ps | grep nginx     (for example)
              (Just like you would on your Mac or pc)

## .


## ......

#### 120. Let's say you know how to run a pod via command line. You can do this very easily because you have done it many times. Given that, how can you quickly generate a YAML file for doing the same thing?

    Answer:  add -o yaml AND --dry-run=client options to the same command.
             This will spit out the YAML file on your terminal.
             You can also redirect that to a file.

## .


## ......

#### 121. You ran: kubectl get po foo -o yaml > foo.yaml .  The problem is that this YAML file has lots on info about the running pod in addition to the "core" yaml content need.  How do you get a clean YAML file out of this?

       Answer: You can delete most of those lines (e.g. the status fields and many others)

## .


## .......

#### 122. What is a clusterrolebinding?

     Answer: It is valid Kubernetes object that links a subject (e.g. an user) to a role.
             This is how a user gets all the permissions that role has. (Much like AWS)

## .


## .......


#### 123. If you want a pod to be associated with a service account name, how do you do it in yaml file?

     Answer: In the "spec" section, add: serviceAccountName foobarserviceaccount
             (Much like in AWS, an ec2 can "assume role", here a pod gets the permissions that the Service Account has)

## .



## ......

#### 124. What does a YAML file for a pod that has 2 containers look like?

     Answer: "containers" section is an array. So, you can define as many containers as you like using dashes.
       Here is an example: 
         apiversion v1
         kind pod
         metadata
           name foo2containers
         spec
           containers
           - image nginx
             name ONE
             env
             - name ONE
             value foo
           - image busybox
             name TWO
             command sleep 1000

## .


## .....

#### 125. How to see what network policies you have in default namespace?

     Answer: kubectl get netpol

## .



## ........

#### 126. Can you use pod selctors in ingres network policy?

     Answer: Yes.

## .



## .......

#### 127. What is the deal with "api-versions". What is the context for this?

     Answer: Kubernetes is not one API. It is set of APIs. As in the case of any large scale development project, each api is it's stage of maturity. This is why 1. you see so many Kubernetes APIs 
     and 2. Each has different versions (alpha, beta etc.)

## .


## ......

#### 128. How to see the correct network api version to use in neteork policy yaml file?
  
     Answer: kubectl api-versions | grep -i network

## .


## ......

#### 129. On a Mac or PC, Where is the default kubectl configuration file?

     Answer: Is located at ~/. kube/config and is referred to as the kubeconfig file

## .


## .......

#### 130. You have a deployment named foo. How can you scale it up via cli: (imperative way) ?

     Answer: kubectl scale deployment foo --replicas=10

## .


## ......

#### 131. You suspect something is wrong with the control plane pods. What should your run?

     Answer: kubectl -n kube-system get pods  
       (to see if any the pods in that namespace is having problems)

## .



## .......

#### 132. You see that a pod is in "imagepullbackoff" state (ie not running),
     what should you look at?

     Answer: You should see which image that pod is configured to use.
             "imagepullbackoff" means that, for some reason, Kubernetes could not pull the docker image.
             This could be because image is not there OR there are permission issues prohibiting the download of that image.

## .



## .......

#### 133. Scenario Question: You issued the command to scale up a deployment to 3 replicas. it is stuck at 3 desired and 1 running.
     You found out that the controller-manager pod on the master had issues. You fixed that so, controller-manager pod
     is now running. What do you have to do next so that scaling finally happens?

     Answer: Nothing! controller-manager starts and does its job

## .


## ......

#### 134. How do you list out all pods running in the namespace foo?

     Answer: kubectl get pods -namespace=foo

## .


## ........

#### 135. What does imperative vs declarative provisioning means in provisioning resources for Kubernetes?

     Answer:
       Imperative: Basically via commands
       Declarative: basically via yaml files

## .


## .......

#### 136. Assume that you are connected to the cluster and context, how do you quickly create an NGINX pod using an imperative approach?

     Answer: kubectl run nginx --image=nginx

## .


## ........

#### 137.  Describe what is namespace in Kubernetes and why is it used?

     Answer: 
       It's like an isolation process. e.g. If you namespaces dev and prod, you can have pods named foo in both namespaces and there is no conflict. (In the same cluster)
       In Kubernetes, you can have the dev team their own namespace and prod can have its own namespace.

## .


## ........

#### 138. You deploy an application to a GKE cluster by applying kubectl -f deployment.yaml.  After deployment you check the pods status and see that the pods are in CrashLoopBack mode.  
          Outline the steps that you use to troubleshoot and the kubectl command you use to diagnose the problem.

     Answer:
       Step 1: run the describe pod command and read through events
       Step 2: run the kubectl logs -p podname and see what is going on with pods (use --previous option, since pod has already crashed)

## .


## ......

#### 139. What are the functions of Kubernetes control plane?  Where do those functions reside?

     Answer: Api server + etcd + scheduler + kube-control-manager + cloud-control-manager
             They run on the master node.

##

#### 140.  What are the components of the worker node?

      Answer: Docker (runtime engine) + kubelet + kube-proxy

## .


## .......

#### 141. Which component of Kubernetes is responsible for tainting and placement of pods on the nodes.

     Answer: scheduler

## .



## .......

#### 142. When a new GKE cluster is created,  what are the main namespaces created?

     Answer: Default and kube-system

## .


## ........

#### 143. What do you use labels and selectors for in Kubernets?

      Answer: So that you can select something based on those labels. They are like tags in AWS. Let's say I want to use node-affinity. We can use labels to select (selector argument in yaml or command) the ones desired.

## .


## .......

#### 144. Examples of  slapping labels on pods

    Answer:
      kubetcl  label pods pod1 owner=mamun
      kubectl  label pods pod2 owner=foo

## .


## .......

#### 145. Examples of using selectors to get pods:

    Answer:
      kubetcl get pods --selector owner=mamun
      kubectl get get pods -l owner=foo

## .



## ........

#### 146. What are annotations use for in Kubernetes and how are they different from labels and selectors  

     Answer:  Non-identifying metadata (e.g. contact info). Almost like comments
              You can't select based on annotations. You can select based on labels.

## .


## .......

#### 147. Is deployment and service the same - Explain the difference or the sameness between the 2 concepts

 
      Answer: No.
         Deployment is like terraform apply (of pods) that you can run a bunch of time with changing configurations (Kubernetes keeps track and so you can roll back).
         Service is basically an entrypoint for users to hit the pods with the right application. Users only know about service and not the pods behind it.

## .


## ........

#### 148. How do pods and service relate to each other.  

     Answer: Service = pods + some ip and ports (there are 3 different kinds, nodeport, clusterip and LB)
             Another way to look at it: service is a persistent front-door to 1 or more pods that can come and go.

## .



## .........

#### 149.  What are the 3 main characteristics you should focus on to troubleshoot what can go wrong between pods and services?

      Answer: Target port (port on containers), labels and selectors

## .



## .........

#### 150. What are the mechanisms to expose an application running in Kubernetes to the outside world?

     Answer: pods ---> service ---> Public IP ---> DNS ---> External Users

## .


## .........

#### 151. How do you check to see if the deployments are ready?

     Answer: kubectl get deployments

## .


## ..........

#### 152. List some useful commands to troubleshoot Pods issues:  (These will come in handy on various interview questions)

     Answer:
       Kubectl describe pod
       Kubectl port-forward podname 3000:80 (example)
       Kubectl get pods -o wide
       Kubectl logs podname
       Kubectl get pod podname
       Kubectl exec -ti podname bash


## .


## .......

#### 153. What is port-forwarding?

     Answer: You make a link between a port on your Mac or PC (localhost) and a port on a pod.
             For example, pod is open on port 443. If you set up port-forward to you localhost port 4430, you can get to the web server on pod via https://localhost:4430

## .



## ........

#### 154. Pods can have startup and runtime errors - Explain what some of these errors mean and 2-3 common culprits  (These wil come in handy for various interview questions)
          Imagine the interviewer asking you about each specific one and you having explain that one.


     Answer:
       ImagePullBackOff
       : the docker image could not be gotten
	       Registry name is bad or not reachable
	       Docker image name is bad or image no longer exists

       CrashLoopBackOff
       : container comes up and crashes/exists
	       Container has nothing to do, so it shuts down
	       Initial value of readiness probe is too small compared to what is needed by container¿s tasks

       RunContainerError
       : container could not be kicked off
	       Pod network solution is not working
	       Authorization Issues

       Pods in Pending State
       : waiting for scheduling for one reason or another
	       Not enough resources on node(s)
	       Worker node cannot reach master node
       
       Pods in a not Ready State
       : pod has been scheduled, but it has not finished coming up for one reason or another
	       There is a readiness probe that's failing

## .


## ........

#### 155.  Can you schedule regular pods on the master node (general Kubernetes, not GKE).  

      Answer: Yes. BUT, the noschedule taint (which is there by default) has to be removed first.

## .



## .........

#### 156. You have a node A with taint=blue.  You have a Pod X with toleration for taint=blue.  Would pod X always be placed on Node A. Explain your answer in detail (Why yes or no)

     Answer:
       Taint is a barrier. The fact that pod X has toleration for blue means that it CAN be scheduled on node A. 
       However, if there are other nodes with no taint or taint of blue, X can land there too.

## .


## ...........


#### 157. What is the use case for node affinity vs nodeSelector?

     Answer:
       nodeSelector is simplistic based on labels whereas node affinity allows much more complex matching, soft-matching and un-matching.
       nodeSelector use cases: pods belonging to a team go on the same node(s). Pods belonging to an environment (e.g. dev) go on the same node(s).
       node affinity use cases: geographic location. Pods go on nodes where some pods live (OR do not live)

## .


## ........

#### 158.  How do you find out what image of the running container (in a pod)?

      Answer: kubectl describe pod podname | grep -i image

## .


## .......

#### 159.  Command used to find out what node the pods are running on:

      Answer: kubectl get pods -o wide

## .



## ........

#### 160. What does the READY column in the output column of the "kubectl get pods" command indicate?

     Answer: How many containers are supposed to run in the pod and how many are actually running.

## .


## ........

#### 161.  What happens if all master nodes are unavailable on (GKE) ? would that impact workloads running on the worker nodes?

      Answer:  Workloads will keep running. However, no new deployments can be pushed. No fault tolerance using replicasets 
               (scheduler is down) will happen. This is the same as Hadoop.

## .


## ......

#### 162.  Why are worker nodes spread out on multiple availability zones in GKE?

      Answer:
        If Google Cloud has an outage in one AZ, application will still be available.

## .


## .......

#### 163. What is the difference between setting up a GKE cluster as regional versus zonal.  This will require you read up on GKE implementation of K8s

     Answer:
       Multi-zonal cluster: master is present in only one zone + nodes are in N zones
       Regional cluster: masters are present in N zones + nodes are in N zone
       So, In Regional cluster, master is HA at the regional level, whereas in Multi-zonal cluster, it is not.

## .


## ......

#### 164. What is the difference between a daemonset and a deployment?

     Answer: Sometimes there is a need to have some pods on EVERY node (e.g. DNS server or a log collector). One can deploy these ¿sets¿ as a daemon set on each node.
             Deployment is a declarative definition of replicasets/pods. You define what needs to go on (how many, what type etc) and the deployment controller ensures that the "desired state" is always there.

## .


## ........

#### 165. What is the default deployment strategy of a Kubernetes deployment?

     Answer: Default is Rolling Update.
             Some other are:
               Blue-green deployment
               Canary deployment
               A/B testing

## .


## .......

#### 166. In a replica set definition how do we tell the replica set that a set of pods is part of the replica set?

     Answer: Using Selectors:
       e.g.
       spec:
         replicas: 3
         selector:
	       matchLabels
## .


## .......

#### 167. How to add a node pool?  (in GCP)

    Answer: gcloud container node-pools create $NAME --cluster $CLUSTER --region $REGION

## .


## .......

#### 168. What namespace does kube-scheduler reside in?

    Answer: kube-system

## .



## ........

#### 169. Does "kubectl pods -help"   work? 

    Answer: no, because kubectl does not recognize "pods" as valid 2nd level command

## .



## .......

#### 170. What are the benefits of the resource limits in Kubernetes ?

  Answer: 
    This is the way to make sure the containers do not consume more resources than desired. This way, 2 things can happen:
    Runaway containers do no affect others
    We get alerted when resource increase over time does not reach a certain limit.

## .


## ........

#### 171.  True/False:  Resource limits are set on per-pods basis in Kubernetes

      Answer:  False. They are set at container level.

## .


## .......

#### 172. Explain what is meant by resource request and resource limits setting.

     Answer: 
       Request: amount of resources a container asks for and scheduler only schedules IF that amount IS available on a node. ("entrypoint")
       Limit: container is killed or throttled IF a container ever tries to get this much resource.("bad boy level")

## .


## ........

#### 173. How to filter "kubectl get pods" output by label?

     Answer:  kubectl get pods -l env=dev
         (to filter by label env matching "dev")

## .



## .......

#### 174. How to "deploy" 3 exact same pods (via YAML file)  

     Answer: In the spec section of the yaml: (for pod)
             spec:
               replicas: 3

## .


## ........

#### 175. True/False: A POD is not a scalable unit (imperatively). A Deployment that schedules PODs is.

     Answer: True 

## .


## .......

#### 176. Why would you have many Deployments work together in the virtual network of the cluster?

     Answer: There are many use cases for this. One example would be to deploy many micro-services. Each micro-service would be a deployment. 

## .


## ......

#### 177. To expose a pod so that users can get to it, you need to create ________ ?

     Answer: Service

## .



## .......

#### 178. You can think of Ingress as ________

     Answer: Layer 7 LB  (or AWS API Gateway)

## .


## .......

#### 179. Deployments are meant to contain stateless services. If you need to store a state you need to create ________ instead (e.g. for a database service).

     Answer: StatefulSet

## .


## .......

#### 180.  How do you see which pods or nodes are using the most resources?

    Answer: kubectl top pod   OR
            kubectl top nodes

## .


## .......

#### 181.  Can a POD span more than 1 "node" ?

      Answer: No

## .


## .......

#### 182. Does a Pod always get an IP?

     Answer: Yes

## .



## .......

#### 183. Let's say that you want to add a "sleep" command to your container. Where does that go in the YAML file?

     Answer: in spec section:  command: ['sleep']

## .


## ........

#### 184. What is the format for ConfigMap?

     Answer: key-value pair (just like almost anything else :-) )

## .


## ........

#### 185. Can you edit any live object using "kubectl edit" command?

     Answer: No

## .



## ........

#### 186. Command to edit the configuration of a live pod:

     Answer: kubectl edit pod foo
## .


## ........

#### 187. Command to delete a running pod:

     Answer: kubectl delete foo

## .


## ......

#### 188. What dictates how much resources does a container get?

     Answer: request and limit parameters

## .
 


## .......

#### 189. Pods come and go. So, how in the world, does Kubernetes provide any real service?

     Answer: Service's IP NEVER changes. You can point DNS to it. Behind the "service" are the ephemeral pods.

## .



## ........

#### 190. (Real Interview Question asked 2022): You run "k get po" and you ass a pod that is in "completed" state. What does that mean?

     Answer: This means that pod came up, did its job and finished. It did not crash. It is not running. You can still get to its logs


## .  


## .......

#### 191. (Real Interview Question asked 2022): What kind of troubleshooting have you done in Kubernetes?

     Answer: This depends on your experience, but some ideas include ingress, capacity, pods crashing, slow service, certificate expiring etc.

## .  



## ........ 

#### 192. (Real Interview Question asked 2022): How is Anthos Service Mesh compared to Istio?

     Answer: Anthos Service Mesh is managed service. It is cheap ($50 a month for 100 endpoints per cluster as of Jan 2022). It comes with dashboards automatically. So, definitely a good choice. Also, no more hassles of upgrading Istio.

## .  


## .........  

#### 193. Who manages virtual IPs of services?

     Answer: kube-proxy

## .   


## .........  

#### 194. What component of Kubernetes is basically a crude Load Balancer?

     Answer: service

## .   


## ..........  

#### 195. in GKE, how is Ingress implemented by default?

     Answer:  a Load Balancer behind the scene

## .   


## ........  

#### 196. Ingress works at which OSI layer?

     Answer:  Layer 7 (HTTP or HTTPS)

## .   


##  ........... 

#### 197. Validating YAML file is a pain? How do you do that?

     Answer:  Open Source Tools like Terrasan or Kubeval work great.

## .   


## ..........  

#### 198. Where does kube-proxy run?

     Answer:  On each node. You can think of this as any other network proxy (e.g. HAProxy or Nginx or Squid) running on each node managing traffic in and out of nodes.

## .  


##  ......... 

#### 199. Why are there 3 versions of NGINX ingress controller for Kubernetes?

     Answer:  1. One made by Kubernetes Community
              2. One made by Nginx (Open Source)
              3. One made by Nginx (NOT Free)


## .   


## .......  

#### 200. Why would you go with Nginx Ingress Controller (and not the Kubernetes Community One)

     Answer:  With Nginx one, you get HTTP Load Balancing (You don't get with community one)
     Source: https://www.youtube.com/watch?v=OM_N0jjghqI

## .


## ............  

#### 201. When impleneting Prometheus, why is it best use the Adapter pattern?

     Answer: Because otherwise, you will have re-write each application "data" to the format that Prometheus expects. The prometheus sidecar will do that and send the data along w/o you having to modify the application container.

## .


## ............

#### 202. What is Kubelet and where does it run?

     Answer:  Main agent on the worker nodes 

## .



##  ...........

#### 203. (Actual interview question 2022): What is the difference between Docker Compose and Kubernetes ?

     Answer:  Docker Compose: Simple way to run multi-container Docker Applications (defined in YAML file)
              Kubernetes: It is a full-fledge Orchestration Tool

## .



##  ........

#### 204. What is kubeadm used for?

     Answer:  To deploy Kubernetes on existing VMs kind of by hand (running commands for master node and worker nodes)

## .



## .......... 

#### 205. When we run "kubectl run pods" , that gets to the API server on the master node. What does the API server do with that request?

     Answer:  It gives it to the kubelet on one worker node

## .


## .......... 

#### 206. How do you combine kubectl and jsonpath to get the info you need?

     Answer:  You use -o=jsonpath="......blah...." to basically query the output that you get from kubectl to get precisely what you need.

## .

## .......... 

#### 207. How do you deploy a stateless application on Kubernetes?

     Answer: Simply use "deployments"  (Not statefulset  or replicasets)

## .


## .......... 

#### 208. What is an endpoint in Kubernetes?

     Answer: Nothing but an IP and a port. That's it.

## .


## .......... 

#### 209. What is the relationship between a Service and Endpoint?

     Answer: When a client hits a Service, Service needs to know where to send the request to (much like a Load Balancer). It forwards it to an Endpoint.
             When a Service is created based on a "match" with a pod (or pods), Kubernetes automatically creates an Endpoint to the pod's IP and port.
             SERVICE ---> ENDPOINT (automaticlaly created) --> POD'S IP and PORT

## .


## .......... 

#### 210. How can you access the kubelet API?

     Answer:  Two ways:
              1. Using a curl command and pointing to 10250 port of a worker node OR
              2. Opensource tool called kubeletctl

## . 


## .......... 

#### 211. How can you verify that your binary executables (Kubernetes) have not been corrupted?

     Answer:  Create SHA256 Hash  of the binary and compare the message digest with the one given on the official web site.

## . 


## .......... 

#### 212. (Not really an interview question, more a real life question) . You are trying to run a pod with "kubectl run" command, but running into issues with exact formats and options, what do you do (besides googling)?

     Answer:  kubectl run -h

## . 


## .......... 

#### 213. (Not really an interview question, more a real life question) . When you are creating a pod using "kubectl run" command, How can you supply a command to run on the container (like sleep 3600)

     Answer:  Simply supply the command with --command -- option.  
              e.g. kubectl run foo --image=nginx --command -- sh -c "sleep 3600"

## . 


## .......... 

#### 214. How can you login into a pod (assuming it only has 1 container) ?

     Answer: kubectl exec foo -it /bin/bash

## . 


## .......... 

#### 215. When you create a pod you can give it 3 restart options. What are they?

     Answer: 1. Always
             2. Never
             3. OnFailure

## . 


## .......... 

#### 216. When you create a pod you can give it 3 restart options. What are the use cases for each?

     Answer: 1. Always (for Deployments or Replicasets)
             2. Never  (for one time pod runners e.g. via command line)
             3. OnFailure (for "jobs")

## . 


## .......... 

#### 217. If there is a pod already running and you want to restart using a DIFFERENT image, how do you do that using command line?


      Answer: kubectl set image command

## . 


## .......... 

#### 217. When your run k get pods , how do you sort by name?

      Answer: k get pods --sort-by=.metadata.name 
              (Credit Bachina Labs)

## . 


## .......... 

#### 218. When your run k get pods , how do you sort by creationtime?

      Answer: k get pods --sort-by=.metadata.creationTimestamp
              (Credit Bachina Labs)
              (Now you get the idea that you can sort by almost any metadata)

## . 


## .......... 

#### 219. In the YAML file for a pod that has more than 1 containers, how do they container specs show up?

       Answer: As a array. Each element of that array is a container specs.

## . 


## .......... 

#### 220. In the YAML file , what is always the first line?

       Answer: apiVersion:

## . 



## .......... 

#### 221. In the YAML file , how do you define what you are building (pod. replicaset, secret, etc.) ?

       Answer: Second Line has kind:    (e.g. kind: pod)

## . 


## .......... 

#### 222. How to get logs from a container (not a pod) via command line?

       Answer: (An example):  kubetcl get logs foopod -c foocontainer

## . 


## .......... 

#### 223. What does an "operator" pod do?

       Answer: Imagine if you had a set of pods that did MYSQL for you. You would have a leader pod and several read-only pods etc. If a reader pod crashed, a human will have to 
               go in and restart it. If the leader pod carshed, a human would find a way to get it up and running or promote a read-only pod to a leader pod. In Kubernetes stateful sets, an operator 
               pod would do all of that automatically.

               Often a vendor sells you a pod-based solution that requires stateful sets, vendor would include such an operator pod so that you (user/client) will not have to worry about the inner 
               workings on the setup. (I have seen this first hand at companies)

## . 


## .......... 

#### 224. What is CRD?

       Answer: Custom Resource Definition. You wanted to create your own type of resource (like pod, rs, depployments etc), you use CRD to define your own resource type.
               Operators use CRD.

## . 


## .......... 

#### 225. Command to get a list of contexts you have defined:

       Answer: kubectl config get-contexts

## . 


## .......... 

#### 226. Which file holds your context definitions?

       Answer: ~/.kube/config

## . 


## .......... 

#### 227. By default, pod A in namesapce A can talk to pod B in Namespace B. True?

       Answer: Yes

## . 


## .......... 

#### 228. What is the esiest quickest way to create a service for a running pod?

       Answer: Use the kubetcl expose command

## . 


## .......... 

#### 229. What is a Headless service in Kubernetes?

       Answer:  A headless service is a service with a service IP but instead of load-balancing it will return the IPs of our associated Pods.
                Source: https://dev.to/kaoskater08/building-a-headless-service-in-kubernetes-3bk8

## . 

## .......... 

#### 230. If you are using minikube or kubeadm etc., what is a big limitation in terms or Load Balancing?

       Answer:  There is no integrated load balancers (as you would have in AWS or GCP)

## . 


## .......... 

#### 231. When does Kubernetes pull new version of image upon Pod creation ?

        Answer:  if either 
                 1. Using images tagged :latest
                 2. imagePullPolicy: Always is specified

        Source: https://stackoverflow.com/questions/33112789/how-do-i-force-kubernetes-to-re-pull-an-image


## . 

## .......... 

#### 232. What is super quick way to create a service pointing to a running pod?

        Answer:  kubectl expose command

## . 


## .......... 

#### 232. capabilities configuration in XML file, goes where? Pod or Containers?

        Answer:  Conatiners

## . 



## .......... 

#### 233. Why do we need Ingress when we alrady have "service" that can send traffic to many pods of the same type?

        Answer:  One big reason is this: Without Ingress, you would have to have a Load Balancer for every single web application you are hosting in your cluster.
                 That can get very expensive and hard to manage.
                 With Ingress , you can have ONE load balancer that can take in traffic for many web applications and forward them to the right pods.

## . 


## .......... 

#### 234. In the kube confi file, what does the URL point to? (for each context)

        Answer:  URL of the API Server (port is almost always :6443)

## . 


## .......... 

#### 235. For deployments, the default replica count is ___ ? 

        Answer:  1.   (If you want 1, then you cna leave out that option in an imperative command)

## . 


## .......... 

#### 236. How can you update the image of a running deployment using an imperative command ?

        Answer: kubectl set image command

## . 


## .......... 

#### 237. What is the default update method for deoloyments ?

        Answer:  Rolling Update

## . 


## .......... 

#### 238. In the definition of a service what is "port" and what is "Target Port"?

        Answer:  Port : Port on the incoming requests
                 Target Port: Port on the pod where the trafic ends up 
                 (Just like a Load Balancer Configuration)

## . 


## .......... 

#### 239. Your pod uses a Config Map. How Can you automatically restart pod if the Config Map changes?

        Answer:  For this, you have to use deployment. In the config of the deployment, use the CM.
                 When CM changes, and the new CM values breaks things, Deployment is smart enough NOT to scale down.
                 BUT, if the new CM does NOT break things, deployment will scale down and up with the new value.

## . 


## .......... 

#### 240. How do you secure kubernetes?

        Answer:  Big Topic, but 7 major parts:
                 1. Application Security (Ingress, access to pods etc.)
                 2. Devsecops (CICD Pipeline, who gets to deploy where and under what conditions)
                 3. User access (RBAC) etc
                 4. Data Compliance (HIPPA, SOX etc.)
                 5. Keeping the secrets secure 
                 6. Patching Nodes (OS Level)
                 7. Container Image Scanning (automated and regular)

## . 



## .......... 

#### 241. How to you manage costs on Kubernetes? 

        Answer:  3 parts
                 1. Control Pane (Not much you can do)
                 2. Worker Nodes (making sure you are autoscaling)
                 3. Optimal usage of cpu/memory by pods (use Metrics Server or open source tool kubecost)

## . 


## .......... 

#### 242. What is rehrydating? 

        Answer:  (For example , when you are moving to a newer version of Kubernetes), running the same cluster using NEW nodes which is running newer version of Kubernetes and THEN running the pods on the new nodes
                 (Opposite of draining)

## . 


## .......... 

#### 243. Command to drain a node?

        Answer:  kubectl drain ......

## . 


## .......... 

#### 244. How did you monitor your Kubernetes Clusters?

        Answer:  Prometheus and Kibana Combinaion is very common (open source)
                 Other paid options:
                   Dynatrace & Datadog

## . 


## .......... 

#### 245. How do containers on the same pod communicate?

        Answer:  Over localhost!

## . 


## .......... 

#### 246. What are 4 components of the Control Pane?

        Answer:  1. API Server
                 2. Scheduler
                 3. etcd
                 4. Controller Manager

## . 

## .......... 

#### 247. What does Controller Manager do?

        Answer:  Runs the un-ending Kubernetes Loop

## . 


## .......... 

#### 248. If you create an ingress , how will the traffic be impacted?

        Answer:  Nothing! Until you have a Ingress Controller , an ingress rule does nothing.

## . 


## .......... 

#### 249. Does Ingress Controller need to read packets?

        Answer:  Yes, it needs to read the headers

## . 


## .......... 

#### 250. How do you create an Ingress Controller? Provide an example.

        Answer:  You can create a deployment using nginx image. That would be one ay of doing it.

## . 


## .......... 

#### 251. How do you tell an Ingress to use an Ingress Controller?

        Answer:  In the Spec section, there is a configuration item called "backend". There you can point to a service (e.g. based on nginx deployment)

## . 


## .......... 

#### 252. When to use Docker Compose?

        Answer:  When you need to run multiple containers (locally or or on cluster) , and you do not want to keep typing "docker run ....".
                 By the way, these containers can share a volume.

## . 



## .......... 

#### 253. How does a pod get any permission do anything?

        Answer:  Every pod comes with default service account , which in turns gives the pod a token. Whatever permissions that token has, that is what a pod can do.

## . 



## .......... 

#### 254. What is the relationship between a Service Account and a Secret?

        Answer:  Every Service Account automatically gets a secret (no different than any other secret). So, when you create a Service Account, if you do "kubectl get secrets", you will see one for that Service Account.

## . 



## .......... 

#### 255.  When you create Nginx Ingress Controller via YAML file, what would be the "Kind" ?  (e.g. pod, secret, service ....)

        Answer:  LoadBalancer    (You can also run a "Deployment" of those for roubustness"

## . 


## .......... 

#### 256. How can you create an YAML file on the fly without creating a resource ?

        Answer:  Use --dry-run=client option with -o yaml option (kubectl)

## . 


## .......... 

#### 257. How do you deploy 3rd-party applications (built on Kubernetes) to your cluster?

        Answer:  Helm Charts. It has become industry standard for deploying 3rd party applications.  For deploying your own apps to your own Kubernetes Cluster, you may choose something else because Helm is very easy to use. 
                 Theere is a learning curve.

## . 



## .......... 

## 258. What if you want to GitOps adn you want you "desired" kubernetes configs in your git repo AND you want to have a pipeline for deploying kubernetes Infrastructure as soon as new Merge happens? How do you do that?

       Answer:  There two tools for doing this: ArgoCD or flux

## . 


## .......... 

## 259. Managing certificates for all domains for all the apps that live on your cluster is a pain. How do manage those certs and their expirations?

       Answer: (Example answer:  cert-manager.io)  

## . 


## .......... 

## 260. You have Kubernetes ANd other items like databases etc. How do you deploy these as Infrastructure as Code?

       Answer: Best tool for this is Crossplane . 

## .



## .......... 

## 261. How did you implement Observability into your Kubernetes Cluster(s)?

       Answer: There are many options:
               1. Prometheus and Grafana
               2. Datadog
               3. Dynatrace

## .


## .......... 

## 262. How did you collects from your Kubernetes Cluster?

       Answer: Example answer: Promtail
               Datadog can do it, too.

## .


## .......... 

## 263. Where did your ship your logs to?

       Answer: Example answers:
               Loki
               Datadog

## .


## .......... 

## 264. Tools for Policy Management via Admission Controllers:


        Answer:  Kyverno
                 OPA Gatekeeper

 
## .


## .......... 

## 265. You are setting a new image for deployment imperatively. How can you make sure you can rollback if needed?


        Answer:  Use the --record option

 
## .


## .......... 

## 266. What is THE key difference between deployments and StateFullSets (besides keeping state)?


        Answer:  StateFulSets use volumeclaimtemplates. That is the key difference. This way, each pod has acccess to the same data.

 
## .......

#### 267. You have web application hostend on containers on Kubernetes. This web app is accessed via a domain e.g. foobar.com.  You need to add a SSL certificate to somewhere in your Kubernetes infrastructure for this domain.
          Walk me through how you would accomplish that.

     Answer:  This page does a fantastic job of explaning step by step with lots of details.
              https://devopscube.com/configure-ingress-tls-kubernetes/

              Summary:
              1. Get a certificate (either self-signed or otherwise)
              2. deploy the application in Kubernetes cluster (this should already be done)
              3. create a TLS secret in Kubernetes
              4. add TLS block to ingress object
              5. Validate using simple curl command (e.g. curl https://foobar.com -kv  )

## .



## .......

#### 268. What if you want to to actively prohibit pods of certain type to be created (e.g. previleged containers)? How do you accomplish that?

     Answer:

          Use admission controllers

## .


## .......


#### 269. What is an admission controller?

     Answer: Essentially a plugin that intercepts requests to API server and takes action based on what is being requested (e.g. creation of pods)

## .


## .......

#### 270. What is Pod Security Policy?

     Answer: From official docuementation:
     A Pod Security Policy is a cluster-level resource that controls security sensitive aspects of the pod specification. The PodSecurityPolicy objects define a set of conditions that a pod must run with in order to 
     be accepted into the system, as well as defaults for the related fields.

## .


## ......

#### 271. Can you use password to authenticate to API server?

     Answer: Yes, but disabled by default

## .

## ......

#### 272. Can you use x509 certificated to authenticate to API server?

     Answer: Yes, but disabled by default

## .


## ......

#### 273.  Easiest to get a bearer token for Kubernetes  API server auth.

     Answer: Create a Service Account

## .


## ......

#### 274.  How to set up authentication for Kubernetes?

     Answer: Just use GCP IAM

## .


## ......

#### 275. How to rotate your cluster credentials using gcloud CLI?

     Answer:  gcloud containers cluster foo update ¿start-credentials-rotation

## .


## ......

#### 276. How does API Server authenticate a request for object creation in etcd?

     Answer: Client Certificate

## .


## ......

#### 277. How can you a list of types of resources (like pods, secrets, nodes, services and lot more)

     Answer:  kubectl get API-resources 

## .


## ......

##### 278.  What is the MAIN difference between stateless and stateful sets (in terms of what is being used in Kubernetes) ?


      Answer:  Stateful sets use volumeclaimtemplates. That is the key difference.

## .



## ......

#### 279. What are the main 3 things that a worker node will run?

     Answer:
       Kubelet
       Proxy
       Caontainer Run Time Engine

## .


## .....

#### 280. Inside a worker node who keeps the desired state? 

     Answer: kubelet

## .



## ......

#### 281. kublet receives it¿s work in the form of _______  ?

     Answer: YAML

## .



## ......

### 282. Kube Proxy runs on each worker node. For all practical purposes, what is it, really?

    Answer: It is basiclaly a Load Balancer


## .



## ......

#### 283. How can ONE service expose MULTIPLE deployments ?

     Answer: It can do that based on tags?

## .




## .......

### 284.  What does a adapter sidecar do basically ?

    Answer:  Adapter sidecar changes format of output

## .



## ......

### 285.  What are nginx ingress controllers , basically? 

    Answer:  Just a "deployment" of modified version of nginx conatiners.
             e.g. https://github.com/kubernetes/ingress-nginx/blob/main/docs/examples/static-ip/nginx-ingress-controller.yaml

## .



## ......

### 286. How can you have a VM (kubernetes node ) that is small in size and does not any extra packages (e.g. 100s of MBs instead of Gig+)?

    Answer: You can convert a Docker container image (e.g. Ubuntu) and add 2 packages (one of them is a File System package)

## .


## ......

### 287. How can you convert a Docker image to a VM

    Answer: ?????

## .














