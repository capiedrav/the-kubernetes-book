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
* To delete a pod(s): ```kubectl delete pod {pod-name} [{pod-name}]...``` or ```kubectl delete -f {pod-manifest-file} [{pod-manifest-file}]...```
* To delete a service(s): ```kubectl delete svc {service-name} [{service-name}]...```
## Chapter 5 - Virtual Clusters and Namespaces
* To list api resources: ```kubectl api-resources```
* To list namespaces: ```kubectl get namespaces``` or ```kubectl get ns```
* To inspect a namespace: ```kubectl describe ns {namespace}```  
**Note:** You can  add ```-n``` or ```--namespace``` to ```kubectl``` commands to filter results against a specific Namespace. For example:
* ```kubectl get svc --namespace {namespace}``` equivalently ```kubectl get svc -n {namespace}```  
You can also use the ```--all-namespaces``` flag to return objects from all Namespaces.
* To create a namespace imperatively: ```kubectl create ns {namespace}```
* To create a namespace declaratively, define it using a manifest file (.yml) file and run: ```kubectl apply -f {namespace-manifest-file}```
* To delete a namespace: ```kubectl delete ns {namespace}```
* To set ```kubectl``` to automatically run commands against a specific namespace: ```kubectl config set-context --current --namespace {namespace}```
* To delete a namespace: ```kubectl delete ns {namespace}``` **Caution:** deleting a namespace automatically delete objects as pods, services, etc. associated with that namespace.
After deleting a namespace don't forget to reset ```kubectl``` to use the *default* namespace ```kubectl config set-context --current --namespace default```
## Chapter 6 - Kubernetes Deployments
* To create (apply) a deployment: ```kubectl apply -f {deployment-manifest-file}```
* To get inspect a deployment: ```kubectl get deploy {deployment-name}``` or ```kubectl describe deploy {deployment-name}```
* To list ReplicaSets: ```kubectl get rs```
* To inspect a ReplicaSet: ```kubectl describe rs {replicaset-name}```
* To manually scale a deployment (imperatively): ```kubectl scale deploy {deployment-name} --replicas {number-of-replicas}``` **Caution:** This is not the recomended way to scale a deployment, instead update and re-apply the deployment's manifest file.  
* To perform a rolling update: Update and re-apply the deployment's manifest file, i.e., ```kubectl apply -d {updated-deployment-manifest-file}```
* To monitor the rollout process: ```kubectl rollout status deployment {deployment-name}```
* To pause the rollout process: ```kubectl rollout pause deploy {deployment-name}```
* To resume the rollout process: ```kubectl rollout resume deploy {deployment-name}```
* To list the rollout history of a deployment: ```kubectl rollout history deployment {deployment-name}```
* To rollback a deployment (imperatively): ```kubectl rollout undo deployment {deployment-name} --to-revision={revision-number}``` **Caution:** This is not the recomended way to rollback a deployment, instead update and re-apply the deployment's manifest file.
* To delete a deployment: ```kubectl delete -f {deployment-manifest-file}``` 

