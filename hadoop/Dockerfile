FROM centos

ENV HADOOP_VERSION 2.7.3

RUN yum -y update; yum clean all
RUN yum install -y java java-devel git tar ssh rsync which openssh-server; yum clean all
RUN /usr/sbin/alternatives --list|grep java_sdk_openjdk|tail -1|awk '{print "export JAVA_HOME="$NF}' >> ~/.bashrc 
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''  && \
    ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N '' && \
    ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N ''

RUN MIRROR=`curl -sSL https://www.apache.org/dyn/closer.cgi\?as_json\=1 | grep preferred|awk -F'"' '{print $(NF-1)}'`  && \
    echo $MIRROR && \
    HADOOP_DOWNLOAD=$MIRROR/hadoop/common/stable/hadoop-${HADOOP_VERSION}.tar.gz &&\
    curl "$HADOOP_DOWNLOAD" >  "/root/hadoop-${HADOOP_VERSION}.tar.gz.tmp"  &&\
    mv /root/hadoop-${HADOOP_VERSION}.tar.gz.tmp /root/hadoop-${HADOOP_VERSION}.tar.gz
   
RUN tar xf /root/hadoop-${HADOOP_VERSION}.tar.gz  -C /opt

COPY conf/* /opt/hadoop-${HADOOP_VERSION}/etc/hadoop/
COPY bin/* /root/
COPY README.md /root/

ENV HADOOP_HOME /opt/hadoop-${HADOOP_VERSION}
ENV PATH $HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH

EXPOSE 8088 50070
