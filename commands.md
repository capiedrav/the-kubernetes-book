# The Kubernetes Book (2024 edition)

## kubectl commands

## Chapter 3 - Getting Kubernetes
* To list nodes: ```kubectl get nodes```
* To show *kubeconfig* file: ```kubectl config view```
* To show current context: ```kubectl config current-context```
* To change the current context: ```kubectl config use context {context-name}```
## Chapter 4 - Working with Pods
* To list all pod attributes: ```kubectl explain pods --recursive```
* To deploy a pod: ```kubectl apply -f {pod-manifest-file}```
* To check the status of a pod(s): ```kubectl get pods [{pod-name}]```
* To check the status of a service(s): ```kubectl get svc [{service-name}]```
* To obtain more details about a pod: ```kubectl get pods {pod-name} -o wide```, ```kubectl get pods {pod-name} -o yaml``` or ```kubectl describe pod {pod-name}```
* To get the logs of a container running inside the pod: ```kubectl logs {pod-name} [--container {container-name}]```
* To execute commands inside a container (remote command execution): ```kubectl exec {pod-name} -- {command} [--container {container-name}]```
* To execute commands inside a container (interactive session): ```kubectl exec -it {pod-name} -- {command} [--container {container-name}]```
* To delete a pod(s) *imperatively*: ```kubectl delete pod {pod-name} [{pod-name}]...``` **Caution:** This is not the recommended way to delete a pod, instead, use the *declarative* way.  
* To delete a pod(s) *declaratively*: ```kubectl delete -f {pod-manifest-file} [{pod-manifest-file}]...```
* To delete a service(s) *imperatively*: ```kubectl delete svc {service-name} [{service-name}]...``` **Caution:** This is not the recommended way to delete a service, instead, use the *declarative* way.
* To delete a service(s) *declaratively*: ```kubectl delete -f {svc-manifest-file} [{svc-manifest-file}]...```  
## Chapter 5 - Virtual Clusters and Namespaces
* To list api resources: ```kubectl api-resources```
* To list namespaces: ```kubectl get namespaces``` or ```kubectl get ns```
* To inspect a namespace: ```kubectl describe ns {namespace}```  
**Note:** You can  add ```-n``` or ```--namespace``` to ```kubectl``` commands to filter results against a specific Namespace. For example: ```kubectl get svc --namespace {namespace}``` equivalently ```kubectl get svc -n {namespace}``` You can also use the ```--all-namespaces``` flag to return objects from all Namespaces.
* To create a namespace *imperatively*: ```kubectl create ns {namespace}```
* To create a namespace *declaratively*, define it using a manifest file (.yml) file and run: ```kubectl apply -f {namespace-manifest-file}```
* To delete a namespace: ```kubectl delete ns {namespace}```
* To set ```kubectl``` to automatically run commands against a specific namespace: ```kubectl config set-context --current --namespace {namespace}```
* To delete a namespace: ```kubectl delete ns {namespace}``` **Caution:** deleting a namespace automatically delete objects as pods, services, etc. associated with that namespace.
After deleting a namespace don't forget to reset ```kubectl``` to use the *default* namespace ```kubectl config set-context --current --namespace default```
## Chapter 6 - Kubernetes Deployments
* To create (apply) a deployment: ```kubectl apply -f {deployment-manifest-file}```
* To get inspect a deployment: ```kubectl get deploy {deployment-name}``` or ```kubectl describe deploy {deployment-name}```
* To list ReplicaSets: ```kubectl get rs```
* To inspect a ReplicaSet: ```kubectl describe rs {replicaset-name}```
* To manually scale a deployment *imperatively*: ```kubectl scale deploy {deployment-name} --replicas {number-of-replicas}``` **Caution:** This is not the recommended way to scale a deployment, instead update and re-apply the deployment's manifest file.  
* To perform a rolling update: Update and re-apply the deployment's manifest file, i.e., ```kubectl apply -d {updated-deployment-manifest-file}```
* To monitor the rollout process: ```kubectl rollout status deployment {deployment-name}```
* To pause the rollout process: ```kubectl rollout pause deploy {deployment-name}```
* To resume the rollout process: ```kubectl rollout resume deploy {deployment-name}```
* To list the rollout history of a deployment: ```kubectl rollout history deployment {deployment-name}```
* To rollback a deployment *imperatively*: ```kubectl rollout undo deployment {deployment-name} --to-revision={revision-number}``` **Caution:** This is not the recommended way to rollback a deployment, instead update and re-apply the deployment's manifest file.
* To delete a deployment: ```kubectl delete -f {deployment-manifest-file}```
## Chapter 7 - Kubernetes Services
* To create (deploy) a service *imperatively*: ```kubectl expose deployment {deployment-name} --type={LoadBalancer|ClusterIp|NodePort}``` **Caution:** This is not the recommended way to create a service, instead, use the *declarative* way.    
* To create (deploy) a service *declaratively*: ```kubectl apply -f {service-manifest-file}``` **Note:** Running minikube on Linux with the Docker driver will result in no tunnel being created. So, to expose the service, use the ```minikube service {service-name} --url``` command. It must be run in a separate terminal window to keep the tunnel open. ```Ctrl-C``` in the terminal can be used to terminate the process at which time the network routes will be cleaned up.   
* To inspect a service: ```kubectl get svc [{service-name}] [-o wide]``` or ```kubectl describe svc {service-name}```
* To inspect endpointslices: ```kubectl get endpointslices [{endpointslice-name}]``` or ```kubectl describe endpointslice {endpointslice-name}```
* To delete a service(s) *imperatively*: ```kubectl delete svc {service-name} [{service-name}]...``` **Caution:** This is not the recommended way to delete a service, instead, use the *declarative* way.
* To delete a service(s) *declaratively*: ```kubectl delete -f {svc-manifest-file} [{svc-manifest-file}]...```
## Chapter 8 - Ingress
* To install the NGINX ingress controller in minikube: ```minikube addons enable ingress```
* To verify that the NGINX ingress controller is running: ```kubectl get pods -n ingress-nginx``` **Note:** It can take up to a minute before these pods are running OK.
* To inspect an ingressclass: ```kubectl get ingressclass [{ingressclass-name}]``` or ```kubectl describe ingressclass {ingressclass-name}```
* To create (deploy) an ingress object *declaratively*: ```kubectl apply -f {ingress-manifest-file}```
* To inspect an ingress object: ```kubectl get ing [{ingress-name}]``` or ```kubectl describe ing {ingress-name}```
* To delete an ingress object: ```kubectl delete -f {ingress-manifest-file}```
## Chapter 10 - Service Discovery Deep Dive
* To list the pods running the cluster DNS: ```kubectl get pods -n kube-system -l k8s-app=kube-dns```
* To show the deployment that manage the pods: ```kubectl get deploy -n kube-system -l k8s-app=kube-dns```
* To show the service in front of the cluster DNS pods (called *kube-dns*): ```kubectl get svc -n kube-system -l k8s-app=kube-dns```
**Important:** Kubernetes configures every container to use the cluster DNS for service discovery. This is done by automatically configuring every container’s
```/etc/resolv.conf``` file with the IP address of the cluster DNS Service. It also adds search domains to append to unqualified names.

 

