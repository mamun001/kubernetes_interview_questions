

# ................... 204 Kubernetes Interview Questions  ....................

## By  Mamun Rashid :: https://www.linkedin.com/in/mamunrashid/ :: Please connect with me.

### Last Updated: 2021.03.09

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

##

#### 2. You have 2 different contexts (A and B). Context A has a secret named foo. Context B does not. What would be a quick way to create the same exact secret in Context B?

     Answer: 
       1. Switch to Context A
       2. kubetcl get secret foo -o yaml > foo.yaml
       3. Switch to Context B
       4. kubectl apply -f foo.yaml


##

#### 3.  There are more than one way to implement Ingress? What did you use to implement Ingress?

    Answer:  So, ingress is IMPLEMENTED by Ingress Controllers. There are at least 12.
             Most common is a Load Balancer. Another popular one is Nginx Ingress Controller.
             See below for a longer list.


##

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

##

#### 5. What is the different between Ingress and Ingress Controller:

    Answer: Ingress Controller FULFILLS ingress requirements

##

#### 6. Most common type of Ingress Controller?

    Answer: Load Balancers


#### 7. Kubernetes as a project supports and maintains which 3 Ingress Controllers?

    Answer: AWS, GCE, and nginx ingress controllers.
            (This is straight from Kubernetes documentation)

##

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

##


#### 9. How would one start up a Kubernetes cluster to deploy containers/pods on (in GCP)?

     Answer: 
       a. via GCP GUI  OR
       b. via GCP cloud shell window OR
       c. gcloud CLI
       d. Terraform
       e. Google Deployment Manager
       

##


#### 10.   If a container keeps crashing, how do you troubleshoot?

    Answer: You can use --previous option with logs command to see the logs of a crashed container.

##


#### 11.  What happens to containers if they use too much cpu or memory?

    Answer: if they use too much memory, they are evicted.
            if they use too much cpu, they are throttled.

##

#### 12.  How do you manage scaling in Kubernetes?

    Answer: 
      This artcile answers it very well:
      https://www.replex.io/blog/kubernetes-in-production-best-practices-for-cluster-autoscaler-hpa-and-vpa

      a. hpa for pods (horizontal pod autoscaler)
      b. vpa for pods (vertical pod autoscaler)
      c. Cluster Autoscaler:
           The cluster autoscaler is a Kubernetes tool that increases or decreases the size of a Kubernetes cluster (by adding or removing nodes), based on the presence of pending pods and node utilization metrics

##

#### 13. How have you used RBAC with Kubernetes ?

    Answer: Answer will depend on your use case. One possible answer is to have service accounts that do certain things within the cluster.
            By the way, RBAC in Kubernetes is just AWS IAM Policies and Bindings. In RBAC, you have subjects (who gets the permission), verbs (what can the subject actually do), and rolebinding (subject linking to roles) and roles.


##

#### 14. If you have 200 micro-services in your clusters, how do you manage security of each one? How do you avoid toil?

    Answer: RBAC is the answer. You define roles. And you place subjects in those roles. Each role then will have access to X Y Z etc. This is really no different than AWS or AD.

##

#### 15. Tell me about the hardest production Kubernetes issue you solved or faced?

    Answer: 

      Your answer will be unique to your experience. But, here is a hypothetical answer.

      There are N micro-services. One of them gets a new version. But, the HPA for those pods are set wrong. Container keep crashing. This causes cascading failures for many other micro-services. 
      Solution: Fix the HPA settings and add circuit-breakers in the consuming micro-services.

##

#### 16. You want to know how to make yaml files for making PODs and you have no access to internet. What do you do?

    Answer: kubectl explain pod --recursive

      It will show you all fields in a mapped kind of fromat so you exacly what field go where

      Simillarly: kubectl explain pv --recursive    (for PVs)

##

#### 17. How can you have SSL certificates in Kubernetes?

    Answer: SSL cert can be a secret. Then that secret can be mounted on a pod and that pod can whatever it wants with it (e.g. host a SSL web site)

##


#### 18. Opensource Tool to switch contexts easily:

    Answer: kubectx

##


#### 19. Opensource menu-driven text-based flexible Tool to manage Kubernetes everything:

    Answer: k9s

##


#### 20. "kubectl explain" command is great, but you must know the exact name of the resource (e.g. pod/services/persistentvolume) to get the details, unless you do recursive. How do you get the names of these resources from command line?

    Answer: kubectl api-resources  (gives you a list and shortnames and more)  

##

#### 21. Name some of the other verbs that kubectl has besides "run" "create" or "apply" ?

         Answer: There are many! Some examples below:

         expose, set , explain, get, edit, delete, rollout, scale, autoscale
         certificate, cluster-info, top, cordon, uncordon, drain, taint
         describe, logs, attach, exec, port-forward, proxy, cp, auth, debug
         diff, apply, patch, replace, wait, kustomize, label, annotate,
         completion, api-resources, api-versions, config, plugin, version

        Some of more frequently used ones are: logs, get, port-forward and label.

##


#### 22. What might you get when you run kubectl api-resources? 

    Answer: api-resources is fancy term. Basically you get stuff like pods/secrets/config-maps all that stuff.

##

##### 23. How else can you get help with kubectl? (besides kubectl explain command)

    Answer: kubectl --help  is actaully better than kubectl explain in my opinion.

##

#### 24. You ran "kubectl --help" , but you want a little more help. What to do?


    Answer:
       kubectl get --help 
       kubectl top --help 
       kubectl describe --help 

##

#### 25. Outline the steps to deploy additional scheduler on a Kubernetes cluster (not GKE)

     Answer:
       Package the new scheduler in a docker image
       Put that image in a registry
       Create a deploymentment file with type: deployment and component: scheduler (in namespace kube-system)
       Deploy the the scheduler with apply -f scheduler.yaml command

##

#### 26. List out 2 use cases for Daemonsets and explain why it is more appropriate to use daemonset than deployment for those use case:

     Answer:
       1. Pod that collects logs. Better to use daemonsets for this because you can logs to be fed from all pods (e.g. to kibana). Otherwise you have to make this part of EVERY deployment which would be annoying and repetitive.
       2. Pod that runs monitoring (e.g. dynatrace or datadog). Reason is the same as above.

##

#### 27. How to move workload to new nodepool? 

    Answer: cordon and drain
        1. cordon means: dont add any more pods to this nodepool
        2. drain means: move current pods out of it

##  

#### 28. Is ClusterIP private or public?

    Ans: Private

##

#### 29. Which one will allow to access your services from internet: cluster ip or nodeport? 

    Answer:  nodeport. confirmed!  
             why? Because NODE is a VM with an external IP and thus can be reached.
             Cluster IP is 10.x IP (internal)

##

#### 30. For a service, when we use nodeport, EVERY node does what?

    Answer: Gives that service an IP and proxy's it. confirmed 

##

#### 31. What does it mean when we say that a node proxy's a service?

    Answer: The node forwards the traffic to a pod that is part of the service.

##

#### 32. 2 ways to let container have access to a secret: 

   Answer: Volume and ENV variable

##

#### 33. How can a container have access to secret via ENV variable? 

    Answer: You can define a ENV in yaml file just like everyhing else and container can just do echo $WHATEVER

##

### 34. One-liner kubectl commad to run a pod with nginx:alpine 

    Answer:  k run nginx-pod --image=nginx:alpine 

             (nginx-pod is arbitrary pod name)

##

#### 35. One liner command to  run a pod with a label  

    Answer: kubectl run foobar --image=redis:alpine -l label1:foo 

##

### 36. kubectl command to show labels of all pods in default namespace:  

    Answer: kubectl get pods --show-labels 

##

#### 37. Whenever you run a kubectl command, it runs in the the default namespace. How do you make in run in a different namespace?

    Answer: use -n namespace_name   (to whatever kubectl command you are running.)

##

#### 38. Command to create a namespace: 

    Answer: kubectl create ns foobar # create a namespace

##

#### 39. When using kubectl command, how do you to get output in json format?  

    Answer: kubectl get nodes -o json # json format

##


#### 40. kubectl expose command: port VS targetport:  (which one is which ?)

    Answer:
       port : on the cluster
       targetport: on the container (just like ALB)

##

#### 41. Command to expose a pod as a service 

    Answer: kubectl expose pod foobarpod --name foobarservice --port 6379 --target-port 6379  # expose a pod as a service
            (NOTE servicename is specified: foobarservice)

##


#### 42.  Command to get details of a service : 

     Answer: kubectl describe svc foobarservice # get details of that service

##


#### 43. Command to create a deployment from image: foobar/webapp-color 

    Answer: kubectl create deployment foobardeployment --image=foobar/webapp-color 

## 

#### 44. Command to scale deploayment named foobardeployment to 2 replicas  

    Answer: kubectl scale deployment foobardeployment --replicas=2 # scale that to 2 replicas  

##


#### 45. Can you scale a kubernetes service?

    Answer: No. You can scale deployments and replicasets

##

#### 46. If you want your kubernetes command to have a scope of ALL namespaces, how do you do that?

    Answer: add -A to the command

##

#### 47. Are environment variables encrypted in Kubernetes? 

    Answer: No
 
##

#### 48. By default, can a pod in one namespace talk to another pod in another namespace? 

    Answer: Yes.

##

#### 49. How to generate a yaml file from an imperative command you know works ? 

    Answer: add: --dry-run=client -o yaml 

##

##### 50. Write a kubectl command to Create a static pod, have it run a command (so it does not exit). dryrun so that you get yaml file saved : 

    Answer: kubectl run static-busybox --image=busybox --command sleep 1000 --dry-run=client -o yaml > static-pod-busybox.yaml

##

#### 51. By default, where does yaml files for static POD files go:  

    Answer: /etc/kubernetes/manifests/  (on the node)

##


#### 52. What is a static pod?

    Answer: This is from official documentation.  Static Pods are managed directly by the kubelet daemon on a specific node, without the API server observing them.

##

#### 53. Kubectl command to take all the details for a.yaml file and create the resource it tells API to crate: 

    Answer: kubectl apply -f a.yaml  

##

#### 54. Kubectl command to list all the pods in foo namespace: 

    Answer: kubectl get pods -n foo

##

#### 55. There is pod named foo. it is in crashloopbackoff state. How to find the cause using a kubectl command? 

    Answer: kubectl describe pod foo

    # to see why it is in crashlookpbackoff state

    What you might see is for example, container's "command" has a mispelling in it. (Just an example)

##

#### 56. Scenario Question: You have a container that keeps crashing because its "command" section has a misspelling. How do you fix this?

    Answer:
      1. generate the yaml file, 
      2. fix it, 
      3. kill the pod, 
      4. re-run with the correct yaml file (kubectl apply -f)

##

#### 57. How to get a yaml file out of running/crashing pod? 

    Answer: kubectl get pod foo -o yaml > foo.yaml 

##

#### 58. How to terminate a running pod? 

    Answer: kubectl delete pod foo

##

#### 59. Command to see a list of running pods in the default namespace: 

    Answer: kubectl get pods 

##

#### 60. Kubectl command to make a new yaml file for a service by exposing a already running deployment that runs a pod.  Name of the deployment: foo.

    Answer: Kubectl expose deployment foo --name foo-service --type=NodePort --port 8080 --target-port=8080 --dry-run=client -o yaml > svc.yaml

##

#### 61. jsonpath example of getting "everything"  (about nodes)  

    Answer: kubetcl get nodes -o jsonpath='{.items[*]}'   # everything, so tons of data
            * Thing to remember is syntax starts out like awk (single quote and swiggly bracket and then follows dots for JSON levels and [] for lists.

##

#### 62. jsonpath example of getting just the level "status" for all nodes 

    Answer: kubectl get nodes -o jsonpath='{.items[*].status}'   # quite a bit of data comes back

##

#### 63. jsonpath comamnd to get only status.nodeInfo of each node  

    Answer: kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo}'   # better, more managable amount of data

##

#### 64:  Your computer has no access to internet. Which kubectl command  can you use to find out syntax of making a pv.yaml : 

     Answer: kubectl explain pv --recursive  # to find out syntax of making a pv.yaml

##

#### 65. What is the different between PV and PVC?

    Answer: PV is basically a disk volume of some sort.  PVC is a link between that volume and a pod.

##

#### 66. Kubectl command to get a list of PVs

    Answer: kubectl get pv   

##

#### 67. Kubectl command to get detail about a PV   

    Answer: kubectl describe pv foo  

##

#### 68. How does the Master server talk to etcd ?

     Answer: It makes a call etcd (runs on localhost in most cases). To do that, it authorizes itself with etcd using 2 certs and 1 key.
               AND sends commands to etcd.
             On the master node, the file that has these configs is at : /etc/kubernetes/manifests/etcd.yaml
             That file in turn , points to the 2 cert files and 1 key file.

##

#### 69. Some example of commands the master server can send to etcd (once authenticated with certs and key):

     Answer:
       member list
       snapshot save /tmp/etcd-backup.db
       snapshot status /tmp/etcd-backup.db -w table

##

#### 70. Steps to create a pod called foo with image redis with CPU Request set to 2 CPU and Request as 400MiB


       Answer:
         a. first create a yaml file: (dry-run command)
            kubectl run --generator=run-pod/v1 foo --image=redis --dry-run -o yaml > foo.yaml
         b. edit the yaml file:
            in the resources section of "spec" section:
            cpu: 2
            memory: 400MiB
         c. kubectl apply -f ./foo.yaml

##

#### 71. True or False: POD DEFINITION (yaml) ONLY points to PVC (claim), it does not refer to the PV anywhere. 

     Answer: True

##

#### 72. Kubectl command to create deployment with busybox version 1.13  
     
     Answer: kubectl run foo-deploy --image=busybox:1:13 --replica=1 --record  # create deployment w busybox 1.13

##

#### 73. kubectl command to look at deployment's history: 
   
     Answer: kubectl rollout history deployment foo-deploy # look at deployment's history  

##


#### 74. kubectl command to change the image version of a deployment on the fly:  

     Answer:  kubectl set image deployment/foo-deploy busybox:latest --record # CHANGE THE IMAGE VERSION

##


#### 75. Kubectl command to a list of existing deploymnets 

    Answer: kubectl get deployments    

##

#### 76. Why do you need certificates in Kubernetes, anyway?

     Answer: For one thing, the API server won't talk to you , if you don't have a signed client certificate. So, any client who wants to do ANYTHING with the API server (e.g. even kubectl) better have a signed certificate!

     Please read:  https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/

##

#### 77. Why are .csr files have CSR extension?

     Answer: CSR = Certificate Signing Request.  
             For example A needs B to give A a signed certificate SO THAT A can later talk to B using that certificate. A will send a CSR (Certificate Signing Request) to B. The file that A sends to be will be CSR and thus will have .csr extension.

             Please read:  https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/

##

#### 78. Why does Kubernetes have certificate API ?

     Answer: So that the certificate signing process can be automated end to end.

##

#### 79. What's an easy way lookup kubernetes documenation on the fly simply using kubectl command?

     Answer: kubectl explain   

##

#### 80. Kubernetes Security: How are some of the ways you can protect your container images?

     Answer:
       a. Update them (to get latest security patches at the OS level)
       b. Scan them regularly
       c. Sign them digitally

##

#### 81. Can you think of some general areas of Kubernetes where you would want to think about security:

     Answer:
       a. Your container images
       b. Your container registry
       c. Your kubernetes run time infrastructure (e.g. etcd)
       d. Hosts (where Kubernetes nodes are running)
       e. Kubernetes Secrets
       f. Kubernetes Certificates
       g. RBAC entities

##

#### 82. Processes within a container: How to they (security-wise) talk to API server running on the master node?

     Answer: Using a Kubernetes Service Account

##

#### 83. What does base64 command do?

     Answer: it "encodes" a file or strings.

     Note: The reason why this is related to Kubernetes is that sometimes you use this command to encode soemthing before putting it in the yaml file.

##


#### 84. How do you generate a CSR within the Kubernetes system?

     Answer: 
       a. create a .csr file
       b. encode it
       c. create a yaml file (Kind: CertificateSigningRequest) using the encoded CSR
       d. kubectl apply -f CertificateSigningRequest.yaml

##

#### 85. If you have created CertificateSigningRequest, but you have not approved it yet, what status do you get if you run "kubectl get csr" command?  

     Answer: You will see that the request is in "pending state"

##

#### 86. Command to approve a CSR? 

     Answer: kubectl certificate approve foo-csr   
      
       Example output:  certificatesigningrequest.certificate.k8s.io/foo-csr approved

##

#### 87. Kubectl command to create role:

     Answer:  kubetcl create role

       A detailed example: kubectl create role foo --resource=pods --verb=create,list,get,update,delete --namespace=development
                           role.rbac.authorization.k8s.io/foo created

##


#### 88. Command to describe a role: 

     Answer: kubectl describe role foo -n foo_namespace  

##

#### 89. Why is important to keep etcd secure and encrypted?

     Answer: etcd data store all your Kubernetes data including Kubernetes secrets

##

#### 90. Which component of Kubernetes has to have "certificate authority" ?

     Answer: Master Node  (because clients will authenticate with the API server using client certificates)

##

#### 91. 3 Steps for creating a CA (Certificate Authority) on master node?

    Answer: (On a managed Kubernetes like GKE and EKS, you don't need to do this):
      a. create a private key
      b. create CSR
      c. self-sign the CSR

##

#### 92. Can you run etcd over HTTP?

  Answer: Yes, but horrible idea, basically all traffic do and from etcd will not be encrypted

##

### 93. Command to insert and Key-Value (foo=bar) pair into etcd?

  Answet: etcdctl put foo "bar"

##

#### 94. When you tell Kubernetes to run a pod, who decides which node gets that pod?

  Answer: Scheduler

##

#### 95. What if you don't like the default scheduler that comes with Kubernetes?

  Answer: You can always run your own schdeluer

##

#### 96. If a node has taint, what you have to do to your pod, for it to be able to run on that node?

  Answer: You have to give the pod the same toleration

##

#### 97. If you want a pod to run on specific node, which feature do you have to use?

  Answer: Node Affinity

##

#### 98. If we already have a liveness probe, why do we need a readiness probe?

  Answer: There are times, when a container fails liveness probe and yet we do not want to container to be killed. For example, if a container takes time to ready (loads large data set). In this case, liveness probe would fail and (without a readiness probe), Kubernetes would kill the container. A readiness probe tell Kubernetes to wait for the container finish doing all its prep work.

##

#### 99. What does it mean for Kubernetes to drop support for Docker?

  Answer: Best answer is given here:  https://kubernetes.io/blog/2020/12/02/dont-panic-kubernetes-and-docker/ . Summary is that, you would have switch to other run time (e.g. containerd or CRI-O) by the time Kubernetes 1.22 comes around. 

##

#### 100. What is "logging driver" ?

  Answer: Docker has the ability to send logs to various places (e.g. awslogs or fluent and many more). Each one of these is a logging driver.

##

#### 101. Which component collects and aggregates the metrics ?

  Answer: cAdvisor (which is part of kubelet on worker nodes)
            Those are then sent to Metric Server (running on master nodes). Metrics Server exposes them via kube-api (also running on the master node)

##

#### 102. When you run "kubetcl top", which component are you talking to?

     Answer: kube-api (which gets its data from metric server)

##

#### 103. By default, conatiner runs with with what UID?

     Answer: 0  (i.e. root).  This can be potentially bad, in case container is somehow able to get a hold of the host OS.

##

#### 104. What is the idea behind "Security Context" ?

     Answer: Security Context is what level of permissions we give the container as it runs. BY default, it runs with UID 0, which is potentially bad. Be using runAsUser, runAsGroup and fsGroup, we can limit what can the container do on the host. This is "Security Context"

##

#### 105. What is "Ambassador Pattern" ?

     Answer: When the sidecar proxy's the connections from the main container to the outside world.

##

#### 106. What is "Adapter Pattern" ?

     Answer: When the sidecar re-formats the output of the application running on the main container to another desired format.
               This way, you don't have to re-write the application code when there is need to re-format the output for some other system to consume.

##

#### 107. Can you describe a use-case where the ambassador pattern can be of use?

     Answer: If you have legacy application which cannot be modified, BUT you have a need to change to the port on which this app needs to listen on, the ambassador container can listen on the new port and pass on the traffic to the old port which did not get modified.

##

#### 108. What is the difference between a label and selector?

     Answer: Labels are basically tags. Selectors use key-value pairs to pick out objects (e.g. pods) to work on.

##

#### 109. What is a network policy in Kubernetes?

     Answer: A network policy is equivalent to a Security Group in AWS. You define who can talk to who via network policy.

##

#### 110. Network Policies often rely on what?

    Answer: labels and selectors

##

#### 111. When do maxSurge and maxUnavailable come in to play?

    Answer: In Rolling Updates of Deployments.
            maxSurge tells Kubernetes how many (or percent) extra pods it can create during rolling update.
            mxUnavailable tells Kubernetes how many (or percent) pods can be unavailable during the rolling uodate.

##

#### 112. Why do we need HPA when we already have maxSurge and maxUnavailable?

    Answer: HPA is an autoscaling thing. maxSurge and maxUnavailable only apply during rolling updates.

##

#### 113. Difference between Service Port and Target Port?

     Answer: Service Port is where users come to get the micro-service. Target Port is the port of the container/pod where the application listens and exposes. 

##

#### 114. You are configuring a service and you have made a mistake with labels and/or selectors. How does this manifest itself often?

     Answer: You will see the service and there will be no endpoint.

##

#### 115. You are logged in to conext via kubectl on your Mac. How can you see if you have permission to update pods? 

       Answer: kubectl auth can-i update pods   
               (You get back: yes)

##

#### 116. Let's say you manage 100 GKE Clusters. You want to run a kubectl command. How do you make sure your command will be executed on the right cluster?

     Answer: You will have 100 contexts (one for each cluster you have logged in to). You must switch to to the right context before running the command.  There is a open-source CLI tool called kubectx that helps you with this.

##

#### 117. What is a super quick way to create a service?

     Answer: Using a kubectl expose command

        Example: kubectl expose pod foopod --name=fooservice --port=80 --target-port=80 --type=ClusterIP
                 :: service/ngnix-resolver-service exposed

##

#### 118. How does Kubernetes do DNS interally?

       Ans: kube-system namespace has pod(pods) that DNS servers.
            You can see them by running: kubectl get po -A | grep dns

##

#### 119. If you are on a node, how do you look for running container? 

     Answer:  docker ps | grep nginx     (for example)
              (Just like you would on your Mac or pc)

##

#### 120. Let's say you know how to run a pod via command line. You can do this very easily because you have done it many times. Given that, how can you quickly generate a YAML file for doing the same thing?

    Answer:  add -o yaml AND --dry-run options to the same command.
             This will spit out the YAML file on your terminal.
             You can also redirect that to a file.

##

#### 121. You ran: kubectl get po foo -o yaml > foo.yaml .  The problem is that this YAML file has lots on info about the running pod in addition to the "core" yaml content need.  How do you get a clean YAML file out of this?

       Answer: You can delete most of those lines (e.g. the status fields and many others)

##

#### 122. What is a clusterrolebinding?

     Answer: It is valid Kubernetes object that links a subject (e.g. an user) to a role.
             This is how a user gets all the permissions that role has. (Much like AWS)

##


#### 123. If you want a pod to be associated with a service account name, how do you do it in yaml file?

     Answer: In the "spec" section, add: serviceAccountName foobarserviceaccount
             (Much like in AWS, an ec2 can "assume role", here a pod gets the permissions that the Service Account has)

##

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

##

#### 125. How to see what network policies you have in default namespace?

     Answer: kubectl get netpol

##

#### 126. Can you use pod selctors in ingres network policy?

     Answer: Yes.

##

#### 127. What is the deal with "api-versions". What is the context for this?

     Answer: Kubernetes is not one API. It is set of APIs. As in the case of any large scale development project, each api is it's stage of maturity. This is why 1. you see so many Kubernetes APIs and 2. Each has different versions (alpha, beta etc.)

##

#### 128. How to see the correct network api version to use in neteork policy yaml file?
  
     Answer: kubectl api-versions | grep -i network

##

#### 129. On a Mac or PC, Where is the default kubectl configuration file?

     Answer: Is located at ~/. kube/config and is referred to as the kubeconfig file

##

#### 130. You have a deployment named foo. How can you scale it up via cli: (imperative way) ?

     Answer: kubectl scale deployment foo --replicas=10

##

#### 131. You suspect something is wrong with the control plane pods. What should your run?

     Answer: kubectl -n kube-system get pods  
       (to see if any the pods in that namespace is having problems)

##

#### 132. You see that a pod is in "imagepullbackoff" state (ie not running),
     what should you look at?

     Answer: You should see which image that pod is configured to use.
             "imagepullbackoff" means that, for some reason, Kubernetes could not pull the docker image.
             This could be because image is not there OR there are permission issues prohibiting the download of that image.

##

#### 133. Scenario Question: You issued the command to scale up a deployment to 3 replicas. it is stuck at 3 desired and 1 running.
     You found out that the controller-manager pod on the master had issues. You fixed that so, controller-manager pod
     is now running. What do you have to do next so that scaling finally happens?

     Answer: Nothing! controller-manager starts and does its job

##

#### 134. How do you list out all pods running in the namespace foo?

     Answer: kubectl get pods -namespace=foo

##

#### 135. What does imperative vs declarative provisioning means in provisioning resources for Kubernetes?

     Answer:
       Imperative: Basically via commands
       Declarative: basically via yaml files

##

#### 136. Assume that you are connected to the cluster and context, how do you quickly create an NGINX pod using an imperative approach?

     Answer: kubectl run nginx --image=nginx

##

#### 137.  Describe what is namespace in Kubernetes and why is it used?

     Answer: 
       It's like an isolation process. e.g. If you namespaces dev and prod, you can have pods named foo in both namespaces and there is no conflict. (In the same cluster)
       In Kubernetes, you can have the dev team their own namespace and prod can have its own namespace.

##

#### 138. You deploy an application to a GKE cluster by applying kubectl -f deployment.yaml.  After deployment you check the pods status and see that the pods are in CrashLoopBack mode.  Outline the steps that you use to troubleshoot and the kubectl command you use to diagnose the problem.

     Answer:
       Step 1: run the describe pod command and read through events
       Step 2: run the kubectl logs -p podname and see what is going on with pods (use --previous option, since pod has already crashed)

##

#### 139. What are the functions of Kubernetes control plane?  Where do those functions reside?

     Answer: Api server + etcd + scheduler + kube-control-manager + cloud-control-manager
             They run on the master node.

##

#### 140.  What are the components of the worker node?

      Answer: Docker (runtime engine) + kubelet + kube-proxy

##

#### 141. Which component of Kubernetes is responsible for tainting and placement of pods on the nodes.

     Answer: scheduler

##

#### 142. When a new GKE cluster is created,  what are the main namespaces created?

     Answer: Default and kube-system

##

#### 143. What do you use labels and selectors for in Kubernets?

      Answer: So that you can select something based on those labels. They are like tags in AWS. Let's say I want to use node-affinity. We can use labels to select (selector argument in yaml or command) the ones desired.

##

#### 144. Examples of  slapping labels on pods

    Answer:
      kubetcl  label pods pod1 owner=mamun
      kubectl  label pods pod2 owner=foo

##

#### 145. Examples of using selectors to get pods:

    Answer:
      kubetcl get pods --selector owner=mamun
      kubectl get get pods -l owner=foo

##

#### 146. What are annotations use for in Kubernetes and how are they different from labels and selectors  

     Answer:  Non-identifying metadata (e.g. contact info). Almost like comments
              You can't select based on annotations. You can select based on labels.

##

#### 147. Is deployment and service the same - Explain the difference or the sameness between the 2 concepts

 
      Answer: No.
         Deployment is like terraform apply (of pods) that you can run a bunch of time with changing configurations (Kubernetes keeps track and so you can roll back).
         Service is basically an entrypoint for users to hit the pods with the right application. Users only know about service and not the pods behind it.

##

#### 148. How do pods and service relate to each other.  

     Answer: Service = pods + some ip and ports (there are 3 different kinds, nodeport, clusterip and LB)
             Another way to look at it: service is a persistent front-door to 1 or more pods that can come and go.

##

#### 149.  What are the 3 main characteristics you should focus on to troubleshoot what can go wrong between pods and services?

      Answer: Target port (port on containers), labels and selectors

##

#### 150. What are the mechanisms to expose an application running in Kubernetes to the outside world?

     Answer: pods ---> service ---> Public IP ---> DNS ---> External Users

##

#### 151. How do you check to see if the deployments are ready?

     Answer: kubectl get deployments

##

#### 152. List some useful commands to troubleshoot Pods issues:  (These will come in handy on various interview questions)

     Answer:
       Kubectl describe pod
       Kubectl port-forward podname 3000:80 (example)
       Kubectl get pods -o wide
       Kubectl logs podname
       Kubectl get pod podname
       Kubectl exec -ti podname bash


##

#### 153. What is port-forwarding?

     Answer: You make a link between a port on your Mac or PC (localhost) and a port on a pod.
             For example, pod is open on port 443. If you set up port-forward to you localhost port 4430, you can get to the web server on pod via https://localhost:4430

##

#### 154. Pods can have startup and runtime errors - Explain what some of these errors mean and 2-3 common culprits  (These wil come in handy for various interview questions)


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

##

#### 155.  Can you schedule regular pods on the master node (general Kubernetes, not GKE).  

      Answer: Yes. BUT, the noschedule taint (which is there by default) has to be removed first.

##

#### 156. You have a node A with taint=blue.  You have a Pod X with toleration for taint=blue.  Would pod X always be placed on Node A. Explain your answer in detail (Why yes or no)

     Answer:
       Taint is a barrier. The fact that pod X has toleration for blue means that it CAN be scheduled on node A. 
       However, if there are other nodes with no taint or taint of blue, X can land there too.

##


#### 157. What is the use case for node affinity vs nodeSelector?

     Answer:
       nodeSelector is simplistic based on labels whereas node affinity allows much more complex matching, soft-matching and un-matching.
       nodeSelector use cases: pods belonging to a team go on the same node(s). Pods belonging to an environment (e.g. dev) go on the same node(s).
       node affinity use cases: geographic location. Pods go on nodes where some pods live (OR do not live)

##

#### 158.  How do you find out what image of the running container (in a pod)?

      Answer: kubectl describe pod podname | grep -i image

##

#### 159.  Command used to find out what node the pods are running on:

      Answer: kubectl get pods -o wide

##

#### 160. What does the READY column in the output column of the "kubectl get pods" command indicate?

     Answer: How many containers are supposed to run in the pod and how many are actually running.

##

#### 161.  What happens if all master nodes are unavailable on (GKE) ? would that impact workloads running on the worker nodes?

      Answer:  Workloads will keep running. However, no new deployments can be pushed. No fault tolerance using replicasets 
               (scheduler is down) will happen. This is the same as Hadoop.

##

#### 162.  Why are worker nodes spread out on multiple availability zones in GKE?

      Answer:
        If Google Cloud has an outage in one AZ, application will still be available.

##

#### 163. What is the difference between setting up a GKE cluster as regional versus zonal.  This will require you read up on GKE implementation of K8s

     Answer:
       Multi-zonal cluster: master is present in only one zone + nodes are in N zones
       Regional cluster: masters are present in N zones + nodes are in N zone
       So, In Regional cluster, master is HA at the regional level, whereas in Multi-zonal cluster, it is not.

##

#### 164. What is the difference between a daemonset and a deployment?

     Answer: Sometimes there is a need to have some pods on EVERY node (e.g. DNS server or a log collector). One can deploy these ¿sets¿ as a daemon set on each node.
             Deployment is a declarative definition of replicasets/pods. You define what needs to go on (how many, what type etc) and the deployment controller ensures that the "desired state" is always there.

##

#### 165. What is the default deployment strategy of a Kubernetes deployment?

     Answer: Default is Rolling Update.
             Some other are:
               Blue-green deployment
               Canary deployment
               A/B testing

##

#### 166. In a replica set definition how do we tell the replica set that a set of pods is part of the replica set?

     Answer: Using Selectors:
       e.g.
       spec:
         replicas: 3
         selector:
	       matchLabels
##

#### 167. How to add a node pool?  (in GCP)

    Answer: gcloud container node-pools create $NAME --cluster $CLUSTER --region $REGION

##

#### 168. What namespace does kube-scheduler reside in?

    Answer: kube-system

##

#### 169. Does "kubectl pods -help"   work? 

    Answer: no, because kubectl does not recognize "pods" as valid 2nd level command

##

#### 170. What are the benefits of the resource limits in Kubernetes ?

  Answer: 
    This is the way to make sure the containers do not consume more resources than desired. This way, 2 things can happen:
    Runaway containers do no affect others
    We get alerted when resource increase over time does not reach a certain limit.

##

#### 171.  True/False:  Resource limits are set on per-pods basis in Kubernetes

      Answer:  False. They are set at container level.

##

#### 172. Explain what is meant by resource request and resource limits setting.

     Answer: 
       Request: amount of resources a container asks for and scheduler only schedules IF that amount IS available on a node. ("entrypoint")
       Limit: container is killed or throttled IF a container ever tries to get this much resource.("bad boy level")

##

#### 173. How to filter "kubectl get pods" output by label?

     Answer:  kubectl get pods -l env=dev
         (to filter by label env matching "dev")

##

#### 174. How to "deploy" 3 exact same pods (via YAML file)  

     Answer: In the spec section of the yaml: (for pod)
             spec:
               replicas: 3

##

#### 175. True/False: A POD is not a scalable unit (imperatively). A Deployment that schedules PODs is.

     Answer: True 

##

#### 176. Why would you have many Deployments work together in the virtual network of the cluster?

     Answer: There are many use cases for this. One example would be to deploy many micro-services. Each micro-service would be a deployment. 

##

#### 177. To expose a pod so that users can get to it, you need to create ________ ?

     Answer: Service

##

#### 178. You can think of Ingress as ________

     Answer: Layer 7 LB  (or AWS API Gateway)

##

#### 179. Deployments are meant to contain stateless services. If you need to store a state you need to create ________ instead (e.g. for a database service).

     Answer: StatefulSet

##

#### 180.  How do you see which pods or nodes are using the most resources?

    Answer: kubectl top pod   OR
            kubectl top nodes

##

#### 181.  Can a POD span more than 1 "node" ?

      Answer: No

##

#### 182. Does a Pod always get an IP?

     Answer: Yes

##

#### 183. Let's say that you want to add a "sleep" command to your container. Where does that go in the YAML file?

     Answer: in spec section:  command: ['sleep']

##

#### 184. What is the format for ConfigMap?

     Answer: key-value pair (just like almost anything else :-) )

##

#### 185. Can you edit any live object using "kubectl edit" command?

     Answer: No

##

#### 186. Command to edit the configuration of a live pod:

     Answer: kubectl edit pod foo
##

#### 187. Command to delete a running pod:

     Answer: kubectl delete foo

##

#### 188. What dictates how much resources does a container get?

     Answer: request and limit parameters

##

#### 189. Pods come and go. So, how in the world, does Kubernetes provide any real service?

     Answer: Service's IP NEVER changes. You can point DNS to it. Behind the "service" are the ephemeral pods.

##

#### 190. (Real Interview Question asked 2022): You run "k get po" and you ass a pod that is in "completed" state. What does that mean?

     Answer: This means that pod came up, did its job and finished. It did not crash. It is not running. You can still get to its logs


##  

#### 191. (Real Interview Question asked 2022): What kind of troubleshooting have you done in Kubernetes?

     Answer: This depends on your experience, but some ideas include ingress, capacity, pods crashing, slow service, certificate expiring etc.

##  



##  

#### 192. (Real Interview Question asked 2022): How is Anthos Service Mesh compared to Istio?

     Answer: Anthos Service Mesh is managed service. It is cheap ($50 a month for 100 endpoints per cluster as of Jan 2022). It comes with dashboards automatically. So, definitely a good choice. Also, no more hassles of upgrading Istio.

##  


##  

#### 193. Who manages virtual IPs of services?

     Answer: kube-proxy

##   


##  

#### 194. What component of Kubernetes is basically a crude Load Balancer?

     Answer: service

##   


##  

#### 195. in GKE, how is Ingress implemented by default?

     Answer:  a Load Balancer behind the scene

##   


##  

#### 196. Ingress works at which OSI layer?

     Answer:  Layer 7 (HTTP or HTTPS)

##   


##  

#### 197. Validating YAML file is a pain? How do you do that?

     Answer:  Open Source Tools like Terrasan or Kubeval work great.

##   


##  

#### 198. Where does kube-proxy run?

     Answer:  On each node. You can think of this as any other network proxy (e.g. HAProxy or Nginx or Squid) running on each node managing traffic in and out of nodes.

##   


##  

#### 199. Why are there 3 versions of NGINX ingress controller for Kubernetes?

     Answer:  1. One made by Kubernetes Community
              2. One made by Nginx (Open Source)
              3. One made by Nginx (NOT Free)


##   


##  

#### 200. Why would you go with Nginx Ingress Controller (and not the Kubernetes Community One)

     Answer:  With Nginx one, you get HTTP Load Balancing (You don't get with community one)
     Source: https://www.youtube.com/watch?v=OM_N0jjghqI

##


## ............  

#### 201. When impleneting Prometheus, why is it best use the Adapter pattern?

     Answer: Because otherwise, you will have re-write each application "data" to the format that Prometheus expects. The prometheus sidecar will do that and send the data along w/o you having to modify the application container.

##


## ............

#### 202. What is Kubelet and where does it run?

     Answer:  Main agent on the worker nodes 

##



##  ...........

#### 203. (Actual interview question 2022): What is the difference between Docker Compose and Kubernetes ?

     Answer:  Docker Compose: Simple way to run multi-container Docker Applications (defined in YAML file)
              Kubernetes: It is a full-fledge Orchestration Tool

##



##  ........

#### 204. What is kubeadm used for?

     Answer:  To deploy Kubernetes on existing VMs kind of by hand (running commands for master node and worker nodes)

##



## .......... 

#### 205. When we run "kubectl run pods" , that gets to the API server on the master node. What does the API server do with that request?

     Answer:  It gives it to the kubelet on one worker node

##







