FROM openjdk:8u151-jdk-alpine3.7
MAINTAINER deven <joshid@gmail.com>

ENV SPARK_VERSION spark-2.3.0
ENV SPARK_RELEASE ${SPARK_VERSION}-bin-hadoop2.7
ENV SPARK_HOME /spark/${SPARK_RELEASE}
ENV PATH ${PATH}:${SPARK_HOME}/bin

RUN apk add --no-cache --update bash curl sed grep procps coreutils && \
    sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd && \
    cd /tmp && \
    curl -jksSLO http://mirrors.sonic.net/apache/spark/${SPARK_VERSION}/${SPARK_RELEASE}.tgz && \
    mkdir /spark && \
    tar zxvf ${SPARK_RELEASE}.tgz -C /spark && \
    rm -rf /var/cache/apk/* /tmp/*

COPY wait-for-it.sh ${SPARK_HOME}/wait-for-it.sh

ADD start-spark-master.sh /sbin/

ADD start-spark-slave.sh /sbin/


WORKDIR ${SPARK_HOME}

CMD ["/bin/bash"]