


docker run --net=host --rm confluentinc/cp-kafka:latest kafka-topics --create --topic foo --partitions 1 --replication-factor 1 --if-not-exists --zookeeper localhost:32181

docker run --net=host --rm confluentinc/cp-kafka:latest kafka-topics --describe --topic foo --zookeeper localhost:32181

docker run --net=host --rm confluentinc/cp-kafka:latest bash -c "seq 42 | kafka-console-producer --broker-list localhost:29092 --topic foo && echo 'Produced 42 messages.'"

docker run --net=host --rm confluentinc/cp-kafka:latest kafka-console-consumer --bootstrap-server localhost:29092 --topic foo --from-beginning --max-messages 42

