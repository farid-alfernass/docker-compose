FROM openjdk:11-jdk

ENV KAFKA_VERSION=2.8.0
ENV KAFKA_HOME=/opt/kafka
ENV PATH=${PATH}:${KAFKA_HOME}/bin

RUN apt-get update && apt-get install -y wget && rm -rf /var/lib/apt/lists/*
RUN wget -q https://archive.apache.org/dist/kafka/${KAFKA_VERSION}/kafka_2.13-${KAFKA_VERSION}.tgz -O /tmp/kafka.tgz
RUN tar xfz /tmp/kafka.tgz -C /opt
RUN rm /tmp/kafka.tgz
RUN ln -s /opt/kafka_2.13-${KAFKA_VERSION} ${KAFKA_HOME}
RUN ./bin/kafka-storage.sh format -t <cluster_id> -c ./config/kraft/server.properties

WORKDIR ${KAFKA_HOME}

CMD ["kafka-server-start.sh", "config/kraft/server.properties"]