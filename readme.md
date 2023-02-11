# Apache ActiveMQ Artemis for multiple architectures

These are prebuilt images of Apache ActiveMQ Artemis to run on amd64 and on older armv7 architecture like the older Raspberry PI 2.

Current Artemis Version :  **2.28.0**

## Quickstart

```
docker run --rm -e JAVA_APPEND_ARGS="-Xms64M -Xmx128M" --name artemis-scratch alainpham/artemis:2.28.0
```

Go to 

http://localhost:8161/metrics/

## From scratch (for custom multi arch builds)

```
cd docker-from-scratch

export ARTEMIS_VERSION=2.28.0

docker build . -t artemis:${ARTEMIS_VERSION}-linux-amd64

docker build . -t artemis:${ARTEMIS_VERSION}-linux-arm-v7

docker tag artemis:${ARTEMIS_VERSION}-linux-amd64 registry.awon.lan/artemis:${ARTEMIS_VERSION}-linux-amd64
docker tag artemis:${ARTEMIS_VERSION}-linux-amd64 alainpham/artemis:${ARTEMIS_VERSION}-linux-amd64

docker push registry.awon.lan/artemis:${ARTEMIS_VERSION}-linux-amd64
docker push alainpham/artemis:${ARTEMIS_VERSION}-linux-amd64

docker tag artemis:${ARTEMIS_VERSION}-linux-arm-v7 registry.awon.lan/artemis:${ARTEMIS_VERSION}-linux-arm-v7
docker tag artemis:${ARTEMIS_VERSION}-linux-arm-v7 alainpham/artemis:${ARTEMIS_VERSION}-linux-arm-v7

docker push registry.awon.lan/artemis:${ARTEMIS_VERSION}-linux-arm-v7
docker push alainpham/artemis:${ARTEMIS_VERSION}-linux-arm-v7



export DOCKER_CLI_EXPERIMENTAL=enabled

docker manifest create registry.awon.lan/artemis:${ARTEMIS_VERSION} \
   -a registry.awon.lan/artemis:${ARTEMIS_VERSION}-linux-amd64 \
   -a registry.awon.lan/artemis:${ARTEMIS_VERSION}-linux-arm-v7

docker manifest push -p registry.awon.lan/artemis:${ARTEMIS_VERSION}

docker manifest create alainpham/artemis:${ARTEMIS_VERSION} \
   -a alainpham/artemis:${ARTEMIS_VERSION}-linux-amd64 \
   -a alainpham/artemis:${ARTEMIS_VERSION}-linux-arm-v7

docker manifest push -p alainpham/artemis:${ARTEMIS_VERSION}

```

```
docker run --rm  artemis:${ARTEMIS_VERSION}-linux-amd64
docker run --rm  artemis:${ARTEMIS_VERSION}-linux-arm-v7

docker run --rm -e JAVA_APPEND_ARGS="-Xms64M -Xmx128M" artemis:${ARTEMIS_VERSION}-linux-amd64
docker run --rm -e JAVA_APPEND_ARGS="-Xms64M -Xmx128M" artemis:${ARTEMIS_VERSION}-linux-arm-v7
```
