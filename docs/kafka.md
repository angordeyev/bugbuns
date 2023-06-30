# Kafka

## Cheat Sheet

Write to a topic

```sh
kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
```

Read a topic

```sh
kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```

## kafdrop

```sh
docker run -d --rm -p 9000:9000 \
    -e KAFKA_BROKERCONNECT=localhost:9000,localhost:9000 \
    -e JVM_OPTS="-Xms32M -Xmx64M" \
    -e SERVER_SERVLET_CONTEXTPATH="/" \
    docker pull obsidiandynamics/kafdrop:4.0.0-SNAPSHOT
```

## Resources

[Apache Quick Start](https://kafka.apache.org/quickstart)
