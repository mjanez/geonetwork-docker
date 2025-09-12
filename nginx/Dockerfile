FROM nginx:stable-alpine

# Variables para GeoNetwork
ENV NGINX_PORT=80
ENV NGINX_LOG_DIR=/var/log/nginx
ENV NGINX_DIR=/etc/nginx
ENV NGINX_SHARE_HTML_DIR=/usr/share/nginx/html
ENV PROXY_SERVER_NAME=localhost

RUN mkdir -p ${NGINX_LOG_DIR} \
    && mkdir -p ${NGINX_DIR}/certs

# Copiar configuración y archivos estáticos
COPY setup/nginx.conf ${NGINX_DIR}/nginx.conf
COPY setup/default.conf.template ${NGINX_DIR}/templates/default.conf.template
COPY setup/geonetwork-docker_local.* ${NGINX_DIR}/certs/
COPY setup/html/index.html ${NGINX_SHARE_HTML_DIR}/

EXPOSE ${NGINX_PORT}