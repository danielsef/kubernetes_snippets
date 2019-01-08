Link:
https://schoolofdevops.github.io/ultimate-kubernetes-bootcamp/3_install_kubernetes/


## Enable Kubernetes Dashboard

After the Pod networks is installled, We can install another add-on service which is Kubernetes Dashboard.

Installing Dashboard:
```
# kubectl apply -f https://gist.githubusercontent.com/initcron/32ff89394c881414ea7ef7f4d3a1d499/raw/4863613585d05f9360321c7141cc32b8aa305605/kube-dashboard.yaml
kubectl apply -f https://gist.githubusercontent.com/danielsef/775abbbb29019e5eccc6183507bf9855/raw/50573ab01eefbfc798eaf0b67c8f97448f946908/kube-dashboard.yaml
```
This will create a pod for the Kubernetes Dashboard.

To access the Dashboard in th browser, run the below command

kubectl describe svc kubernetes-dashboard -n kube-system
Sample output:
```
kubectl describe svc kubernetes-dashboard -n kube-system
Name:                   kubernetes-dashboard
Namespace:              kube-system
Labels:                 app=kubernetes-dashboard
Selector:               app=kubernetes-dashboard
Type:                   NodePort
IP:                     10.98.148.82
Port:                   <unset> 80/TCP
NodePort:               <unset> 31000/TCP
Endpoints:              10.40.0.1:9090
Session Affinity:       None
```
Now check for the node port, here it is 31000, and go to the browser, and access the dashboard with the following URL do not use the IP above, use master node IP instead.

http://MASTER_NODE_IP:31000
