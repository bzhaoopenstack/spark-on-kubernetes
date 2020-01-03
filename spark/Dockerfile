FROM ubuntu:18.04

RUN apt-get update && apt-get install -y git vim curl

RUN apt-get install openjdk-8-jdk -y

#ENV hadoop_ver 2.6.1
ENV hadoop_ver 2.7.4
ENV spark_ver 3.0.0-SNAPSHOT
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-arm64

# Get Hadoop from BIT Apache mirror and extract just the native
# libs. (Until we care about running HDFS with these containers, this
# is all we need.)
RUN mkdir -p /opt
ADD ./hadoop${hadoop_ver}-dist/hadoop-dist/target/hadoop-${hadoop_ver}.tar.gz /opt/
RUN cd /opt && ln -s hadoop-${hadoop_ver} hadoop
#    echo Hadoop ${hadoop_ver} native libraries installed in /opt/hadoop/lib/native

# Get Spark from Apache mirror.
ADD ./spark-${spark_ver}-bin-${hadoop_ver}.tgz /opt/
RUN cd /opt && ln -s spark-${spark_ver}-bin-${hadoop_ver} spark 
#    echo Spark ${spark_ver} installed in /opt

# if numpy is installed on a driver it needs to be installed on all
# workers, so install it everywhere
RUN apt-get update && \
    apt-get install -y python-numpy && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ADD log4j.properties /opt/spark/conf/log4j.properties
ADD start-common.sh start-worker start-master /
ADD core-site.xml /opt/spark/conf/core-site.xml
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf
ENV PATH $PATH:/opt/spark/bin
