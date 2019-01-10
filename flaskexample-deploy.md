
1.) Deployment
kubectl run flaskexample --image=macinv/flask-example --port 8080


2.) Expose Service

kubectl expose deployment flaskexample --port=8080 --target-port=8000
kubectl expose pod f-app --port=8080 --name=f-svc

Examples:
  # Create a service for a replicated nginx, which serves on port 80 and connects to the containers on port 8000.
  kubectl expose rc nginx --port=80 --target-port=8000

  # Create a service for a replication controller identified by type and name specified in "nginx-controller.yaml", which serves on port 80 and connects to the containers on port 8000.
  kubectl expose -f nginx-controller.yaml --port=80 --target-port=8000

  # Create a service for a pod valid-pod, which serves on port 444 with the name "frontend"
  kubectl expose pod valid-pod --port=444 --name=frontend

  # Create a second service based on the above service, exposing the container port 8443 as port 443 with the name "nginx-https"
  kubectl expose service nginx --port=443 --target-port=8443 --name=nginx-https

  # Create a service for a replicated streaming application on port 4100 balancing UDP traffic and named 'video-stream'.
  kubectl expose rc streamer --port=4100 --protocol=udp --name=video-stream

  # Create a service for a replicated nginx using replica set, which serves on port 80 and connects to the containers on port 8000.
  kubectl expose rs nginx --port=80 --target-port=8000

  # Create a service for an nginx deployment, which serves on port 80 and connects to the containers on port 8000.
  kubectl expose deployment nginx --port=80 --target-port=8000
  
  
  
  3.) Ingress
  
  https://medium.com/@Oskarr3/setting-up-ingress-on-minikube-6ae825e98f82
  https://gist.githubusercontent.com/0sc/77d8925cc378c9a6a92890e7c08937ca/raw/84ceff5f03da4a2d0a4d2afabd30a1cf3d61fbd1/ingress-tutorial.yaml
  
  
  
  
  
