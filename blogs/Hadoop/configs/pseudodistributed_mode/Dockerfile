FROM hadoop3:1.0.1

ENV HDFS_NAMENODE_USER="root"
ENV HDFS_DATANODE_USER="root"
ENV HDFS_SECONDARYNAMENODE_USER="root"
ENV YARN_RESOURCEMANAGER_USER="root"
ENV YARN_NODEMANAGER_USER="root"

COPY ./conf $HADOOP_CONF_DIR
RUN echo 'JAVA_HOME=/docker-java-home' >> $HADOOP_CONF_DIR/hadoop-env.sh

RUN apt-get update \
	&& apt-get -y install ssh
