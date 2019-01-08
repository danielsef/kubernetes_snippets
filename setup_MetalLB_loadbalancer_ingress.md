## Setup MetalLB:

Installation With Kubernetes Manifests

To install MetalLB, simply apply the manifest:
```
kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.7.3/manifests/metallb.yaml
This will deploy MetalLB to your cluster, under the metallb-system namespace. The components in the manifest are:
```
The metallb-system/controller deployment. This is the cluster-wide controller that handles IP address assignments.
The metallb-system/speaker daemonset. This is the component that speaks the protocol(s) of your choice to make the services reachable.
Service accounts for the controller and speaker, along with the RBAC permissions that the components need to function.
The installation manifest does not include a configuration file. MetalLB’s components will still start, but will remain idle until you define and deploy a configmap.


metallb-configmap.yaml:
```
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - <NODE MIN IP>-<NODE MAX IP>
```


```
kubectl appply -f metallb-configmap.yaml
```


## Setup ingress:

```
kubectl appply -f  https://gist.github.com/danielsef/50b12c3ade6bfe54dee9dae55223cc52#file-mandatory-ingress-nginx-v2-yaml
kubectl appply -f  https://gist.github.com/danielsef/0fe6e1e5d3e5631efd7ab00337c4620f#file-service-ingress-nginx-v2-yaml
```



## Test Ingress:

https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html






