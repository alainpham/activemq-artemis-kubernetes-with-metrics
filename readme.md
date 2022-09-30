# Apache Activemq Artemis Cloud Container image with Metrics

Aims at fixing the apache activemq artemis cloud container image to add metrics.

Extending https://artemiscloud.io/ images to add metrics plugin for Prometheus monitoring of Artemis.

```
cd docker
 
docker build . -t artemis:1.0.5

```

Run prebuilt image

```
docker run --rm -e AMQ_USER=admin -e AMQ_PASSWORD=admin  -e AMQ_ENABLE_METRICS_PLUGIN=true -p 8161:8161 --name artemis-cloud alainpham/artemis:1.0.5
```

Go to 

http://localhost:8161/metrics/

## From scratch (for custom multi arch builds)

```
cd docker-from-scratch

docker build . -t artemis:2.26.0-linux-amd64

docker build . -t artemis:2.26.0-linux-arm-v7

```

```
docker run --rm artemis:2.26.0-linux-amd64
docker run --rm artemis:2.26.0-linux-arm-v7
```

```

docker manifest create registry.awon.lan/artemis:2.26.0 \
   -a registry.awon.lan/artemis:2.26.0-linux-amd64 \
   -a registry.awon.lan/artemis:2.26.0-linux-arm-v7
docker manifest push
```
