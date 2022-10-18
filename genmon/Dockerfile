ARG GENMON_VERSION=665fb4745e6dd14e318c6cdc093021dbefa8f3d4

FROM python:3.10-slim
ARG GENMON_VERSION

WORKDIR /app
RUN apt-get update \
    && apt-get install -y \
        git \
        sudo \
        make \
    && git clone https://github.com/jgyates/genmon.git . \
    && git checkout ${GENMON_VERSION}
RUN ./genmonmaint.sh -i
RUN pip install spidev
RUN rm -rf /var/log \
    && ln -sf /config/genmon/log /var/log  \
    && ln -sf /config/genmon/config /etc/genmon

CMD bash -c "mkdir -p /config/genmon/log /config/genmon/config && /app/startgenmon.sh -p 3 start && sleep infinity"
