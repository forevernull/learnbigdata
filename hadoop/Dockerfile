FROM centos

RUN yum -y update; yum clean all
RUN yum install -y java java-devel git tar ssh rsync which openssh-server; yum clean all
RUN /usr/sbin/alternatives --list|grep java_sdk_openjdk|tail -1|awk '{print "export JAVA_HOME="$NF}' >> ~/.bashrc 
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''  && \
    ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N '' && \
    ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N ''

RUN git clone https://github.com/forevernull/learnbigdata.git ~/learnbigdata && \
    source ~/.bashrc && cd ~/learnbigdata/hadoop &&  bin/bootstrap


EXPOSE 8088 9000 9870

CMD ["~/learnbigdata/hadoop/bin/bootstrap", "start"]
