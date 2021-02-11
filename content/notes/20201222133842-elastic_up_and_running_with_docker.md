+++
title = "Elastic up and running with docker"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Elasticsearch]({{< relref "20201221151118-elasticsearch" >}})

<!--listend-->

```yaml
version: "3.7"
services:
  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:6.5.1
    container_name: es01
    environment:
      - cluster.name=es-docker-cluster
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - http.cors.enabled=true
      - "http.cors.allow-origin=http://localhost:1358,http://127.0.0.1:1358"
      - "http.cors.allow-headers=X-Requested-With,X-Auth-Token,Content-Type,Content-Length,Authorization"
      - "http.cors.allow-credentials=true"
      - network.host=0.0.0.0
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - es01data:/usr/share/elasticsearch/data
    ports:
      - "9200:9200"
  kibana:
    image: docker.elastic.co/kibana/kibana:6.5.1
    container_name: kibana
    environment:
      - "ELASTICSEARCH_URL=http://es01:9200"
    ports:
      - "5601:5601"
    depends_on: ['es01']
volumes:
  mysqldata:
  redisdata:
  es01data:
```
