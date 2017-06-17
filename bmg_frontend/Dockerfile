FROM artworkad/alpine-node-nightly:latest

MAINTAINER Florian Braun <florianbraun1712@gmail.com>

RUN apk update && \
    apk add --no-cache nginx git supervisor openssh wget gcc g++ make linux-headers python && \
    mkdir -p /var/log/supervisor /root/.ssh && \
    touch /root/.ssh/known_hosts && \
    chown -R nginx:www-data /var/lib/nginx

COPY nginx.conf /etc/nginx/nginx.conf

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
  git clone https://github.com/g0rd0nbl3u/bmg_frontend.git && \
  cd bmg_frontend/frontend && \
  npm install

RUN chown -R nginx:www-data /app/bmg_frontend/frontend

CMD ["/usr/bin/supervisord", "--configuration", "/etc/supervisor/conf.d/supervisord.conf"]
