FROM centos
RUN yum install -y java java-devel git tar ssh rsync
RUN /usr/sbin/alternatives --list|grep java_sdk_openjdk|tail -1|awk '{print "export JAVA_HOME="$NF}' >> ~/.bashrc && source ~/.bashrc
RUN git clone git@github.com:forevernull/learnbigdata.git ~/learnbigdata &&\ 
    cd ~/learnbigdata/hadoop && bin/bootstrap

EXPOSE 9000 9870 8088
