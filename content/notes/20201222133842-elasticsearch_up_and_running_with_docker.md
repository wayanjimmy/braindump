+++
title = "Elasticsearch up and running with docker"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Elasticsearch]({{< relref "20201221151118-elasticsearch" >}}) [Docker]({{< relref "20210518095808-docker" >}})


## Docker compose example {#docker-compose-example}

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


## Troubleshooting {#troubleshooting}


### vm.max\_map\_count [65530] is too low {#vm-dot-max-map-count-65530-is-too-low}

the solution taken from [this](https://github.com/elastic/elasticsearch-docker/issues/92) github issue.

```bash
sudo sysctl -w vm.max_map_count=262144
```

or you can try to edit this permanently, read [more](https://stackoverflow.com/questions/42889241/how-to-increase-vm-max-map-count).
