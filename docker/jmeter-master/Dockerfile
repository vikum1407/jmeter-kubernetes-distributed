FROM vikum1407/jmeter-base:prometheus
LABEL maintainer="vikum1407@sdet"

EXPOSE 60000
ENV SSL_DISABLED true
ENV ONE_SHOT true
ENV SLAVE_SVC_NAME jmeter-slave
ENV SCRIPTS_DIR /scripts

ADD jmeter-script.sh /jmeter-script.sh
RUN chmod +x /jmeter-script.sh \
    && mkdir /scripts

ENTRYPOINT /jmeter-script.sh

