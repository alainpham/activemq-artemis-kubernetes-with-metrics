# apache activemq artemis cloud container image with metrics

Aims at fixing the apache activemq artemis cloud container image to add metrics.

Extending https://artemiscloud.io/ images to add ùetrics plugin for Prometheus monitoring of Artemis.

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