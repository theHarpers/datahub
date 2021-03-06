# Debugging Guide

## How can I confirm if all Docker containers are running as expected after a quickstart?
You can list all Docker containers in your local by running `docker container ls`. You should expect to see a log similar to the below:

```
CONTAINER ID        IMAGE                                                 COMMAND                  CREATED             STATUS              PORTS                                                      NAMES
979830a342ce        keremsahin/datahub-mce-consumer:latest                "bash -c 'while ping…"   10 hours ago        Up 10 hours                                                                    datahub-mce-consumer
3abfc72e205d        keremsahin/datahub-frontend:latest                    "datahub-frontend/bi…"   10 hours ago        Up 10 hours         0.0.0.0:9001->9001/tcp                                     datahub-frontend
50b2308a8efd        keremsahin/datahub-mae-consumer:latest                "bash -c 'while ping…"   10 hours ago        Up 10 hours                                                                    datahub-mae-consumer
4d6b03d77113        keremsahin/datahub-gms:latest                         "bash -c 'dockerize …"   10 hours ago        Up 10 hours         0.0.0.0:8080->8080/tcp                                     datahub-gms
c267c287a235        landoop/schema-registry-ui:latest                     "/run.sh"                10 hours ago        Up 10 hours         0.0.0.0:8000->8000/tcp                                     schema-registry-ui
4b38899cc29a        confluentinc/cp-schema-registry:5.2.1                 "/etc/confluent/dock…"   10 hours ago        Up 10 hours         0.0.0.0:8081->8081/tcp                                     schema-registry
37c29781a263        confluentinc/cp-kafka:5.2.1                           "/etc/confluent/dock…"   10 hours ago        Up 10 hours         0.0.0.0:9092->9092/tcp, 0.0.0.0:29092->29092/tcp           broker
15440d99a510        docker.elastic.co/kibana/kibana:5.6.8                 "/bin/bash /usr/loca…"   10 hours ago        Up 10 hours         0.0.0.0:5601->5601/tcp                                     kibana
943e60f9b4d0        neo4j:3.5.7                                           "/sbin/tini -g -- /d…"   10 hours ago        Up 10 hours         0.0.0.0:7474->7474/tcp, 7473/tcp, 0.0.0.0:7687->7687/tcp   neo4j
6d79b6f02735        confluentinc/cp-zookeeper:5.2.1                       "/etc/confluent/dock…"   10 hours ago        Up 10 hours         2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp                 zookeeper
491d9f2b2e9e        docker.elastic.co/elasticsearch/elasticsearch:5.6.8   "/bin/bash bin/es-do…"   10 hours ago        Up 10 hours         0.0.0.0:9200->9200/tcp, 9300/tcp                           elasticsearch
ce14b9758eb3        mysql:latest
```

Also you can check individual Docker container logs by running `docker logs <<container_name>>`. For `datahub-gms`, you should see a log similar to this at the end of the initialization:
```
2020-02-06 09:20:54.870:INFO:oejs.Server:main: Started @18807ms
```

For `datahub-frontend`, you should see a log similar to this at the end of the initialization:
```
09:20:22 [main] INFO  play.core.server.AkkaHttpServer - Listening for HTTP on /0.0.0.0:9001
```

## How can I check if [MXE](what/mxe.md) Kafka topics are created?

You can use a utility like [kafkacat](https://github.com/edenhill/kafkacat) to list all topics. 
You can run below command to see the Kafka topics created in your Kafka broker.

```bash
kafkacat -L -b localhost:9092
```

Confirm that `MetadataChangeEvent` & `MetadataAuditEvent` topics exist besides the default ones. Example response as below:

```bash
Metadata for all topics (from broker 1: localhost:9092/1):
 1 brokers:
  broker 1 at localhost:9092
 5 topics:
  topic "_schemas" with 1 partitions:
    partition 0, leader 1, replicas: 1, isrs: 1
  topic "__consumer_offsets" with 50 partitions:
    partition 0, leader 1, replicas: 1, isrs: 1
    partition 1, leader 1, replicas: 1, isrs: 1
    partition 2, leader 1, replicas: 1, isrs: 1
    partition 3, leader 1, replicas: 1, isrs: 1
    partition 4, leader 1, replicas: 1, isrs: 1
    partition 5, leader 1, replicas: 1, isrs: 1
    partition 6, leader 1, replicas: 1, isrs: 1
    partition 7, leader 1, replicas: 1, isrs: 1
    partition 8, leader 1, replicas: 1, isrs: 1
    partition 9, leader 1, replicas: 1, isrs: 1
    partition 10, leader 1, replicas: 1, isrs: 1
    partition 11, leader 1, replicas: 1, isrs: 1
    partition 12, leader 1, replicas: 1, isrs: 1
    partition 13, leader 1, replicas: 1, isrs: 1
    partition 14, leader 1, replicas: 1, isrs: 1
    partition 15, leader 1, replicas: 1, isrs: 1
    partition 16, leader 1, replicas: 1, isrs: 1
    partition 17, leader 1, replicas: 1, isrs: 1
    partition 18, leader 1, replicas: 1, isrs: 1
    partition 19, leader 1, replicas: 1, isrs: 1
    partition 20, leader 1, replicas: 1, isrs: 1
    partition 21, leader 1, replicas: 1, isrs: 1
    partition 22, leader 1, replicas: 1, isrs: 1
    partition 23, leader 1, replicas: 1, isrs: 1
    partition 24, leader 1, replicas: 1, isrs: 1
    partition 25, leader 1, replicas: 1, isrs: 1
    partition 26, leader 1, replicas: 1, isrs: 1
    partition 27, leader 1, replicas: 1, isrs: 1
    partition 28, leader 1, replicas: 1, isrs: 1
    partition 29, leader 1, replicas: 1, isrs: 1
    partition 30, leader 1, replicas: 1, isrs: 1
    partition 31, leader 1, replicas: 1, isrs: 1
    partition 32, leader 1, replicas: 1, isrs: 1
    partition 33, leader 1, replicas: 1, isrs: 1
    partition 34, leader 1, replicas: 1, isrs: 1
    partition 35, leader 1, replicas: 1, isrs: 1
    partition 36, leader 1, replicas: 1, isrs: 1
    partition 37, leader 1, replicas: 1, isrs: 1
    partition 38, leader 1, replicas: 1, isrs: 1
    partition 39, leader 1, replicas: 1, isrs: 1
    partition 40, leader 1, replicas: 1, isrs: 1
    partition 41, leader 1, replicas: 1, isrs: 1
    partition 42, leader 1, replicas: 1, isrs: 1
    partition 43, leader 1, replicas: 1, isrs: 1
    partition 44, leader 1, replicas: 1, isrs: 1
    partition 45, leader 1, replicas: 1, isrs: 1
    partition 46, leader 1, replicas: 1, isrs: 1
    partition 47, leader 1, replicas: 1, isrs: 1
    partition 48, leader 1, replicas: 1, isrs: 1
    partition 49, leader 1, replicas: 1, isrs: 1
  topic "MetadataChangeEvent" with 1 partitions:
    partition 0, leader 1, replicas: 1, isrs: 1
  topic "__confluent.support.metrics" with 1 partitions:
    partition 0, leader 1, replicas: 1, isrs: 1
  topic "MetadataAuditEvent" with 1 partitions:
    partition 0, leader 1, replicas: 1, isrs: 1
```

## How can I check if search indices are created in Elasticsearch?

You can run below command to see the search indices created in your Elasticsearch.

```bash
curl http://localhost:9200/_cat/indices
```

Confirm that `datasetdocument` & `corpuserinfodocument` indices exist besides the default ones. Example response as below:

```bash
yellow open .monitoring-es-6-2020.01.27     hNu-jjU3Tl2SKKFdXzjxHQ 1 1 27279 34  14.8mb  14.8mb
yellow open .watcher-history-6-2020.01.27   70BeSxOkQiCsBCGNtZNfAw 1 1  1210  0     1mb     1mb
yellow open corpuserinfodocument            VCupUjstS4SrZHLDruwVzg 5 1     2  0    11kb    11kb
yellow open .monitoring-kibana-6-2020.01.27 pfJy8HOxRQKG-RQKexMKkA 1 1  1456  0 688.3kb 688.3kb
yellow open .watches                        jmJxYOjrSamqlTi-UIrxTA 1 1     4  0  19.6kb  19.6kb
yellow open datasetdocument                 5HB_IpjYSbOh3QUSUeuwgA 5 1     3  0  27.9kb  27.9kb
yellow open .monitoring-alerts-6            qEAoSNpTRRyqO7fqAzwpeg 1 1     1  0   6.2kb   6.2kb
yellow open .triggered_watches              7g7_MGXFR7mBx0FwQzxpUg 1 1     0  0  48.1kb  48.1kb
yellow open .kibana                         HEQj4GnTQauN3HkwM8CPng 1 1     1  0   3.2kb   3.2kb
```

## Getting `cannot start service {X}` error while starting Docker containers.
There can be different reasons why a container fails during initialization. Below are the most common reasons:
### bind: address already in use
This error means that the network port (which is supposed to be used by the failed container) is already in use by your system. You need to find and kill the process which is using this specific port before starting the corresponding Docker container. If, for some reason, you don't want to kill the process which is using that port, another option is to change the port number for Docker container. You need to find and change the [ports](https://docs.docker.com/compose/compose-file/#ports) parameter for the specific Docker container in the `docker-compose.yml` configuration file.

```
Example : On MacOs

ERROR: for mysql  Cannot start service mysql: driver failed programming external connectivity on endpoint mysql (5abc99513affe527299514cea433503c6ead9e2423eeb09f127f87e2045db2ca): Error starting userland proxy: listen tcp 0.0.0.0:3306: bind: address already in use

   1) sudo lsof -i :3306
   2) kill -15 <PID found in step1>
``` 
