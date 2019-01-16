## Setup Kafka and Zookeeper docker images on 10.46.13.136 machine:

docker run -d --name=zookeeper1 -p 2181:2181 -e ZOOKEEPER_CLIENT_PORT=2181 confluentinc/cp-zookeeper:latest
docker run -d --name=kafka1 -p 9092:9092 -e KAFKA_ZOOKEEPER_CONNECT=<hostname>:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://<hostname>:9092 -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 confluentinc/cp-kafka:latest
 
sudo iptables -I INPUT -p tcp --dport 2181 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 9092 -j ACCEPT
 
 
Connection information for Kafka Tools 2.0.2
Zookeeper host: 10.46.13.136
Zookeeper port: 2181

## Run Streamsets on Kuberentes Cluster

kubectl run streamsetsspark --image=dev.docker.5xl/streamsets_spark:1.0 --port=18630 --namespace <namespace>
--overrides='{"spec": { "imagePullSecrets": [{"name": "<secret_name>"}] } }'
kubectl expose deployment streamsetsspark --port=80 --target-port=18630 --name=streamsetsspark-service --type=NodePort --namespace <namespace>
