# Use the specific DinD image version
FROM docker:26.1.3-dind

# Install dependencies and OpenSCAP
RUN apk update && \
    apk add --no-cache \
    openrc \
    python3 \
    build-base \
    libxml2-dev \
    libxslt-dev \
    git && \
    git clone https://github.com/OpenSCAP/openscap.git && \
    cd openscap && \
    ./autogen.sh && \
    make && \
    make install && \
    apk del build-base libxml2-dev libxslt-dev git && \
    rm -rf /var/cache/apk/*

# Set up OpenRC (to run as an init system)
RUN mkdir /run/openrc && touch /run/openrc/softlevel

# Start OpenRC and Docker daemon
CMD ["sh", "-c", "rc-service docker start && /sbin/init"]
