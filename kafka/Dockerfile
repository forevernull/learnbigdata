FROM centos

ENV HADOOP_VERSION 2.7.3

RUN yum -y update; yum clean all
RUN yum install -y java java-devel git tar ssh rsync which openssh-server; yum clean all
RUN /usr/sbin/alternatives --list|grep java_sdk_openjdk|tail -1|awk '{print "export JAVA_HOME="$NF}' >> ~/.bashrc 

# Download Kafka
ENV KAFKA_VERSION 0.10.2.0
RUN MIRROR=`curl -sSL https://www.apache.org/dyn/closer.cgi\?as_json\=1 | grep preferred|awk -F'"' '{print $(NF-1)}'`  && \
    FILE=kafka_2.12-${KAFKA_VERSION}.tgz && \
    HIVE_DOWNLOAD=$MIRROR/kafka/${KAFKA_VERSION}/$FILE &&\
    echo $HIVE_DOWNLOAD && \
    curl "$HIVE_DOWNLOAD" >  "/root/$FILE.tmp"  &&\
    mv /root/$FILE.tmp /root/$FILE

RUN tar zxvf /root/kafka_2.12-${KAFKA_VERSION}.tgz -C /opt 

COPY bin/* /root/bin/

ENV KAFKA_HOME /opt/kafka_2.12-${KAFKA_VERSION}
ENV PATH $KAFKA_HOME/bin:/root/bin:$PATH

EXPOSE 2181 9092
