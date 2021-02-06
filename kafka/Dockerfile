FROM ubuntu:18.04 as kafka_base

WORKDIR /opt/kafka
ENV PATH=$PATH:/opt/kafka/kafka_2.13-2.7.0/bin/

RUN apt-get update && \
    apt-get install -y vim wget maven && \
    wget https://apachemirror.sg.wuchna.com/kafka/2.7.0/kafka_2.13-2.7.0.tgz && \
    tar -xzf kafka_2.13-2.7.0.tgz && \
    rm kafka_2.13-2.7.0.tgz && \
    apt-get install -y openjdk-8-jre-headless && \
    echo "\033[0;32m---------------------" && \
    echo "Checking Java Version" && \
    echo "\033[1;33m" && \
    echo "$(java -version)" && \
    echo "\033[0;32m---------------------\033[0m" && \
    echo "\033[0;32m---------------------" && \
    echo "Checking Maven Version" && \
    echo "\033[1;33m" && \
    echo "$(mvn -version)" && \
    echo "\033[0;32m---------------------\033[0m" && \
    mkdir -p /opt/kafka/scripts && \
    mvn archetype:generate \
    -DarchetypeGroupId=org.apache.kafka \
    -DarchetypeArtifactId=streams-quickstart-java \
    -DarchetypeVersion=2.5.0 \
    -DgroupId=streams.examples \
    -DartifactId=streams.examples \
    -Dversion=0.1 \
    -Dpackage=myapps && \
    rm /opt/kafka/streams-quickstart/src/main/java/myapps/*.java
COPY ./scripts/kafkastreams.java ./scripts/.