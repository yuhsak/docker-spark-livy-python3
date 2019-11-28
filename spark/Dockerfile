FROM openjdk:8

## Vesion

# Spark
ENV SPARK_VERSION=2.4.4
ENV HADOOP_VERSION=2.7
ENV SPARK_VERSION_STRING=spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}
ENV SPARK_HOME=/spark

# Livy
ENV LIVY_VERSION=0.6.0
ENV LIVY_VERSION_STRING=apache-livy-${LIVY_VERSION}-incubating-bin
ENV LIVY_HOME=/livy

# Python
ENV PYTHON_VERSION=3.6.9
ENV PYTHON_VERSION_STRING=Python-${PYTHON_VERSION}

## Source
ADD http://apache.mirror.iphh.net/spark/spark-${SPARK_VERSION}/${SPARK_VERSION_STRING}.tgz /
ADD http://ftp.jaist.ac.jp/pub/apache/incubator/livy/${LIVY_VERSION}-incubating/${LIVY_VERSION_STRING}.zip /
ADD https://www.python.org/ftp/python/${PYTHON_VERSION}/${PYTHON_VERSION_STRING}.tgz  /

## Install
RUN \
	# Spark
	tar xzf ${SPARK_VERSION_STRING}.tgz \
	&& mv ${SPARK_VERSION_STRING} ${SPARK_HOME} \
	&& rm ${SPARK_VERSION_STRING}.tgz \
	# Livy
	&& unzip ${LIVY_VERSION_STRING}.zip \
	&& mv ${LIVY_VERSION_STRING} ${LIVY_HOME} \
	&& mkdir ${LIVY_HOME}/logs \
	&& rm ${LIVY_VERSION_STRING}.zip \
	# Python
	&& apt update \
	&& apt install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev \
	&& tar xzf ${PYTHON_VERSION_STRING}.tgz \
	&& cd ${PYTHON_VERSION_STRING} \
	&& ./configure --enable-optimizations \
	&& make -j `proc` \
	&& make install \
	&& cd / \
	&& rm ${PYTHON_VERSION_STRING}.tgz \
	&& rm -r ${PYTHON_VERSION_STRING} \
	&& apt clean

## Configure
COPY livy.conf ${LIVY_HOME}/conf
COPY spark-env.sh ${SPARK_HOME}/conf

## Ports
# Spark Master
EXPOSE 7077
# Master Web UI
EXPOSE 8080
# Master Livy
EXPOSE 8998