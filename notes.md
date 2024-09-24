# The Kubernetes Book (2024 edition)

## kubectl commands

* To show *kubeconfig* file: ```kubectl config view```
* To show current context: ```kubectl config current-context```
* To change the current context: ```kubectl config use context {context-name}```
* To list all pod attributes: ```kubectl explain pods --recursive```
* To deploy a pod: ```kubectl apply -f {pod-manifest-file}```
* To check the status of a pod: ```kubectl get pods```
* To obtain more details about a pod: ```kubectl get pods {pod-name} -o wide```, ```kubectl get pods {pod-name} -o yaml``` or ```kubectl describe pod {pod-name}```
* To get the logs of a container running inside the pod: ```kubectl logs {pod-name} [--container {container-name}]```
* To execute commands inside a container (remote command execution): ```kubectl exec {pod-name} -- {command} [--container {container-name}]```
* To execute commands inside a container (interactive session): ```kubectl exec -it {pod-name} -- {command} [--container {container-name}]```
* To delete a pod(s): ```kubectl delete pod {pod-name} [{pod-name}]...```
* To delete a service(s): ```kubectl delete svc {service-name} [{service-name}]...```
