FROM eclipse-temurin:11.0.18_10-jre AS builder
ARG artemis_version=2.28.0

USER root

RUN useradd -u 1000 appuser && mkdir -p /home/appuser/ && chown 1000:1000 /home/appuser

ADD distrib/apache-artemis-${artemis_version}-bin.tar.gz /tmp/
RUN mv /tmp/apache-artemis-${artemis_version} /opt/amq 

ADD artemis-prometheus-metrics-plugin-1.1.0.jar /opt/amq/lib/artemis-prometheus-metrics-plugin-1.1.0.jar
ADD metrics.war /opt/amq/web/metrics.war

USER 1000

RUN /opt/amq/bin/artemis create /home/appuser/broker --user admin --password password --allow-anonymous --http-host 0.0.0.0 --no-autotune

ADD bootstrap.xml  /home/appuser/broker/etc/bootstrap.xml
ADD broker.xml  /home/appuser/broker/etc/broker.xml
ADD jolokia-access.xml  /home/appuser/broker/etc/jolokia-access.xml
ADD artemis.profile /home/appuser/broker/etc/artemis.profile

FROM eclipse-temurin:11.0.18_10-jre
RUN useradd -u 1000 appuser && mkdir -p /home/appuser/ && chown 1000:1000 /home/appuser

COPY --from=builder /opt/amq  /opt/amq
COPY --from=builder --chown=1000:1000 /home/appuser/broker /home/appuser/broker

USER 1000

EXPOSE 8161 61616 5445 5672 1883 61613

ENTRYPOINT [ "/home/appuser/broker/bin/artemis", "run" ]
