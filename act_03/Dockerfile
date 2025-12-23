FROM almalinux:9

RUN dnf install -y java-17-openjdk-devel wget tar && dnf clean all

WORKDIR /opt
RUN wget --no-check-certificate https://archive.apache.org/dist/activemq/5.18.3/apache-activemq-5.18.3-bin.tar.gz \
    && tar -xvzf apache-activemq-5.18.3-bin.tar.gz \
    && rm apache-activemq-5.18.3-bin.tar.gz

# Use the REAL path instead of the /opt/activemq symlink
WORKDIR /opt/apache-activemq-5.18.3/lib
RUN rm -f camel-*-*.jar activemq-camel-*.jar

RUN wget --no-check-certificate https://repo1.maven.org/maven2/org/apache/camel/camel-core/2.25.4/camel-core-2.25.4.jar \
    && wget --no-check-certificate https://repo1.maven.org/maven2/org/apache/camel/camel-spring/2.25.4/camel-spring-2.25.4.jar \
    && wget --no-check-certificate https://repo1.maven.org/maven2/org/apache/activemq/activemq-camel/5.16.8/activemq-camel-5.16.8.jar

# Copy configs directly to the real path
COPY activemq.xml /opt/apache-activemq-5.18.3/conf/activemq.xml
COPY camel.xml /opt/apache-activemq-5.18.3/conf/camel.xml

EXPOSE 8161 61616

ENV ACTIVEMQ_OPTS="-Djetty.host=0.0.0.0"
# Point the entrypoint to the real path
ENTRYPOINT ["/opt/apache-activemq-5.18.3/bin/activemq", "console"]