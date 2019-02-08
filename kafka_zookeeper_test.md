## Setup Kafka and Zookeeper docker images on <HOSTNAME> machine:

docker run -d --name=zookeeper1 -p 2181:2181 -e ZOOKEEPER_CLIENT_PORT=2181 confluentinc/cp-zookeeper:5.1.0;

docker run -d --name=kafka1 -p 9092:9092 \
-v /data/docker/logs:/var/lib/kafka/data:rw \
-e KAFKA_ZOOKEEPER_CONNECT=<HOSTNAME>:2181 \
-e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://<HOSTNAME>:9092 \
-e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
confluentinc/cp-kafka:5.1.0;
 
sudo iptables -I INPUT -p tcp --dport 2181 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 9092 -j ACCEPT
 
Connection information for Kafka Tools 2.0.2
Zookeeper host: <HOSTNAME>
Zookeeper port: 2181






##Test Zookeeper and Kafka install:
### Create Topic
docker run \
--rm confluentinc/cp-kafka:latest \
kafka-topics --create --topic foo --partitions 1 --replication-factor 1 \
--if-not-exists --zookeeper <HOSTNAME>:2181;
 
 
### Describe Topic
docker run \
--rm \
confluentinc/cp-kafka:latest \
kafka-topics --describe --topic foo --zookeeper <HOSTNAME>:2181;

### Send message to Topic
 
docker run \
--rm \
confluentinc/cp-kafka:latest \
bash -c "seq 42 | kafka-console-producer --request-required-acks 1 \
--broker-list <HOSTNAME>:9092 --topic foo && echo 'Produced 42 messages.'";
 
### Consume Message from Topic
 
docker run \
--rm \
confluentinc/cp-kafka:latest \
kafka-console-consumer --bootstrap-server <HOSTNAME>:9092 --topic foo --from-beginning --max-messages 42;





## Start Schema Registry
docker run -d \
--net=host \
--name=schema-registry1 \
-e SCHEMA_REGISTRY_KAFKASTORE_CONNECTION_URL=<HOSTNAME>:2181 \
-e SCHEMA_REGISTRY_HOST_NAME=<HOSTNAME> \
-e SCHEMA_REGISTRY_LISTENERS=http://<HOSTNAME>:8081 \
confluentinc/cp-schema-registry:latest;
docker run -it --net=host --rm confluentinc/cp-schema-registry:latest bash




## Start Control Center

docker run -d \
--name=control-center1 \
--net=host \
--ulimit nofile=16384:16384 \
-p 9021:9021 \
-v /tmp/control-center/data:/var/lib/confluent-control-center \
-e CONTROL_CENTER_ZOOKEEPER_CONNECT=<HOSTNAME>:2181 \
-e CONTROL_CENTER_BOOTSTRAP_SERVERS=<HOSTNAME>:9092 \
-e CONTROL_CENTER_REPLICATION_FACTOR=1 \
-e CONTROL_CENTER_MONITORING_INTERCEPTOR_TOPIC_PARTITIONS=1 \
-e CONTROL_CENTER_INTERNAL_TOPICS_PARTITIONS=1 \
-e CONTROL_CENTER_STREAMS_NUM_STREAM_THREADS=2 \
-e CONTROL_CENTER_CONNECT_CLUSTER=http://<HOSTNAME>:8082 \
confluentinc/cp-enterprise-control-center:latest




## Command list:
root@kafka-host:/usr/bin# ls | grep kafka
kafka-acls
kafka-broker-api-versions
kafka-configs
kafka-console-consumer
kafka-console-producer
kafka-consumer-groups
kafka-consumer-perf-test
kafka-delegation-tokens
kafka-delete-records
kafka-dump-log
kafka-log-dirs
kafka-mirror-maker
kafka-preferred-replica-election
kafka-producer-perf-test
kafka-reassign-partitions
kafka-replica-verification
kafka-run-class
kafka-server-start
kafka-server-stop
kafka-streams-application-reset
kafka-topics
kafka-verifiable-consumer
kafka-verifiable-producer
