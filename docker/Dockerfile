FROM quay.io/artemiscloud/activemq-artemis-broker-kubernetes:1.0.5

ADD artemis-prometheus-metrics-plugin-1.1.0.jar /opt/amq/lib/artemis-prometheus-metrics-plugin-1.1.0.jar
ADD metrics.war /opt/amq/web/metrics.war
ADD bootstrap.xml  /opt/amq/conf/bootstrap.xml