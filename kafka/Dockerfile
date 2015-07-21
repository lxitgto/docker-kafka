# Kafka and Zookeeper

FROM ubuntu
MAINTAINER ethan-liu@outlook.com

ENV DEBIAN_FRONTEND noninteractive

# Install Kafka, Zookeeper and other needed things
RUN \
	echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
	echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
	apt-get update && \
	apt-get install -y python-software-properties && \
	apt-get install -y software-properties-common && \
    apt-get install -y zookeeper wget supervisor dnsutils && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    apt-get install -y oracle-java7-installer
    wget -q http://apache.mirrors.spacedump.net/kafka/0.8.1.1/kafka_2.8.0-0.8.1.1.tgz -O /tmp/kafka_2.8.0-0.8.1.1.tgz && \
    tar xfz /tmp/kafka_2.8.0-0.8.1.1.tgz -C /opt && \
    rm /tmp/kafka_2.8.0-0.8.1.1.tgz

ENV KAFKA_HOME /opt/kafka_2.8.0-0.8.1.1
ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf /etc/supervisor/conf.d/kafka.conf
ADD supervisor/zookeeper.conf /etc/supervisor/conf.d/zookeeper.conf

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
