FROM node:8.1.2-alpine

MAINTAINER Florian Braun <florianbraun1712@gmail.com>

RUN apk update && \
    apk add --no-cache git supervisor openssh wget gcc g++ make linux-headers python && \
    mkdir -p /var/log/supervisor /root/.ssh && \
    touch /root/.ssh/known_hosts

# Copy supervisord.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Copy over private key, and set permissions
COPY deploy-key/deploy-key /root/.ssh/id_rsa
RUN chmod 400 /root/.ssh/id_rsa

# Add githubs key
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts

# Define working directory
WORKDIR /app

# Clone the conf files into the docker container
RUN \
  cd /app && \
  git clone https://github.com/g0rd0nbl3u/bmg_backend.git && \
  cd bmg_backend && \
  npm install && \
  mkdir uploads

CMD ["/usr/bin/supervisord", "--configuration", "/etc/supervisor/conf.d/supervisord.conf"]
