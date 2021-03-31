# Simple Kafka Streams Demo

Created the programme based on this [URL](https://kafka.apache.org/quickstart)

## Demo 1
Change directory
```
cd kafka_2.13-2.7.0
```

Start the ZooKeeper service
Note: Soon, ZooKeeper will no longer be required by Apache Kafka.
```
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```

Start the Kafka broker service
```
$ bin/kafka-server-start.sh config/server.properties
```

Create topic
```
$ bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
```

Describe topic
```
bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
```

Start producer
```
bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
```

Start consumer
```
bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```

## Demo 2
Start Zookepper
```
bin/zookeeper-server-start.sh config/zookeeper.properties
```

Start kafka server
```
bin/kafka-server-start.sh config/server.properties
```

Create input topic
```
bin/kafka-topics.sh --create \
    --bootstrap-server localhost:9092 \
    --replication-factor 1 \
    --partitions 1 \
    --topic streams-plaintext-input
 ```
 
 Create output topic
 ```
 bin/kafka-topics.sh --create \
    --bootstrap-server localhost:9092 \
    --replication-factor 1 \
    --partitions 1 \
    --topic streams-wordcount-output \
    --config cleanup.policy=compact
 ```
 
 Describe topics
 ```
 bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe
 ```
 
 Start word count demo application
 ```
 bin/kafka-run-class.sh org.apache.kafka.streams.examples.wordcount.WordCountDemo
 ```
 
 Start producer
 ```
 bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic streams-plaintext-input
 ```
 
 Start consumer
 ```
 bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 \
    --topic streams-wordcount-output \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
  ```
