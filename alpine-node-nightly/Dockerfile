FROM alpine:3.5

MAINTAINER Artjom Zabelin <artjomzabelin@gmail.com>

RUN apk update && \
    apk add --no-cache wget gcc g++ make linux-headers python

# Install nodejs v8.0 nightly from source
RUN wget https://nodejs.org/download/nightly/v8.0.0-nightly20170120ba776b3a56/node-v8.0.0-nightly20170120ba776b3a56.tar.gz --no-check-certificate && \
    tar -zxf node-v8.0.0-nightly20170120ba776b3a56.tar.gz && \
    cd node-v8.0.0-nightly20170120ba776b3a56 && \
    ./configure && \
    make -j4 && \
    make install
