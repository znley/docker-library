FROM lcr.loongnix.cn/openanolis/anolisos:23.1
MAINTAINER pader "huangmnlove@163.com"

# set environment
ENV MODE="cluster" \
    PREFER_HOST_MODE="ip"\
    BASE_DIR="/home/nacos" \
    CLASSPATH=".:/home/nacos/conf:$CLASSPATH" \
    CLUSTER_CONF="/home/nacos/conf/cluster.conf" \
    FUNCTION_MODE="all" \
    JAVA_HOME="/usr/lib/jvm/java-17-openjdk" \
    NACOS_USER="nacos" \
    JAVA="/usr/lib/jvm/java-17-openjdk/bin/java" \
    JVM_XMS="1g" \
    JVM_XMX="1g" \
    JVM_XMN="512m" \
    JVM_MS="128m" \
    JVM_MMS="320m" \
    NACOS_DEBUG="n" \
    TOMCAT_ACCESSLOG_ENABLED="false" \
    TIME_ZONE="Asia/Shanghai"

ARG NACOS_VERSION=2.2.0-BETA
ARG HOT_FIX_FLAG=""

WORKDIR $BASE_DIR

RUN set -x \
    && yum update -y \
    && yum install -y tar java-17-openjdk java-17-openjdk-devel wget iputils nc vim libcurl
RUN wget  http://cloud.loongnix.cn/releases/loongarch64/alibaba/nacos/2.2.0-BETA/nacos-server-2.2.0-BETA.tar.gz -P /home
RUN tar -xzvf /home/nacos-server-${NACOS_VERSION}.tar.gz -C /home \
    && rm -rf /home/nacos-server-${NACOS_VERSION}.tar.gz /home/nacos/bin/* /home/nacos/conf/*.properties /home/nacos/conf/*.example /home/nacos/conf/nacos-mysql.sql
RUN yum autoremove -y wget \
    && ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone \
    && yum clean all




ADD bin/docker-startup.sh bin/docker-startup.sh
ADD conf/application.properties conf/application.properties


# set startup log dir
RUN mkdir -p logs \
	&& cd logs \
	&& touch start.out \
	&& ln -sf /dev/stdout start.out \
	&& ln -sf /dev/stderr start.out
RUN chmod +x bin/docker-startup.sh

EXPOSE 8848
ENTRYPOINT ["bin/docker-startup.sh"]
