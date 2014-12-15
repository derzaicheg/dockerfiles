FROM dockerfile/java:oracle-java7

MAINTAINER Sergii Kozlov "derzaicheg@gmail.com"


# Install Jetty
RUN wget -O /opt/jetty.tar.gz "http://eclipse.org/downloads/download.php?file=/jetty/9.0.7.v20131107/dist/jetty-distribution-9.0.7.v20131107.tar.gz&r=1"
RUN tar -xvf /opt/jetty.tar.gz -C /opt/
RUN rm /opt/jetty.tar.gz
RUN mv /opt/jetty-distribution-9.0.7.v20131107 /opt/jetty
RUN rm -rf /opt/jetty/webapps.demo
RUN useradd jetty -U -s /bin/false
RUN chown -R jetty:jetty /opt/jetty
ADD http://tomcat.apache.org/tomcat-6.0-doc/appdev/sample/sample.war /opt/jetty/webapps/

# Run Jetty
EXPOSE 8080
CMD ["java", "-Djetty.home=/opt/jetty", "-jar", "/opt/jetty/start.jar"]


