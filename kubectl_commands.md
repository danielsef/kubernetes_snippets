
Some useful commands

Get help with kubectl commands:

$ kubectl help

Get the state of your cluster:

$ kubectl cluster-info

Get all the nodes of your cluster:

$ kubectl get nodes -o wide

Get information about the pods of your cluster:

$ kubectl get pods -o wide

Get information about the replication controllers of your cluster:

$ kubectl get rc -o wide

Get information about the services of your cluster:

$ kubectl get services

Get full configuration information about a service:

$ kubectl get service <instancename> -o json

Get the IP address of a pod:

$ kubectl get pod <instancename> -template={{.status.podIP}}

Delete a pod:

$ kubectl delete pod NAME

Delete a service:

$ kubectl delete service <instancename>

Useful links

kubectl reference - https://kubernetes.io/docs/reference/

kubectl cheat sheet - https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/
