FROM alpine:3.10
LABEL maintainer="vikum1407@sdet"

ENV JMETER_VERSION "5.4"

RUN apk update && \
    apk upgrade && \
    apk add --update openjdk8-jre wget tar bash && \
    wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz \
    && tar -xvzf apache-jmeter-${JMETER_VERSION}.tgz \
    && rm apache-jmeter-${JMETER_VERSION}.tgz \
    && mv apache-jmeter-${JMETER_VERSION} /jmeter \
    && rm -rf /var/cache/apk/* \
    && wget -O /usr/bin/tpl https://github.com/schneidexe/tpl/releases/download/v0.4.4/tpl-linux-amd64 \
    && chmod +x /usr/bin/tpl

# Download the jmeter-prometheus-plugin JAR file
RUN wget -O /jmeter/lib/ext/jmeter-prometheus-plugin.jar https://github.com/johrstrom/jmeter-prometheus-plugin/releases/download/0.6.2/jmeter-prometheus-plugin-0.6.2.jar

ENV JMETER_HOME /jmeter

# Add Jmeter to the Path
ENV PATH $JMETER_HOME/bin:$PATH
