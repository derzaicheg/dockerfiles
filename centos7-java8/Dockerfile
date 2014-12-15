FROM centos:centos7

MAINTAINER Sergii Kozlov "derzaicheg@gmail.com"

RUN yum -y install wget
RUN yum -y install tar

WORKDIR /opt
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-x64.tar.gz"

RUN tar -zxf jdk-8u25-linux-x64.tar.gz

RUN alternatives --install /usr/bin/java java /opt/jdk1.8.0_25/bin/java 2
RUN alternatives --auto java

RUN export JAVA_HOME=/opt/jdk1.8.0_25
RUN export JRE_HOME=/opt/jdk1.8.0_25/jre
RUN export PATH=$PATH:/opt/jdk1.8.0_25/bin:/opt/jdk1.8.0_25/jre/bin

CMD java -version


