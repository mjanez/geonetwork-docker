# geonetwork-docker

This repository provides a simple Docker Compose setup to deploy GeoNetwork with Nginx and PostGIS for local development.

## Services

| Service      | Docker Image                                   | Description                        | Container Name      |
|--------------|------------------------------------------------|------------------------------------|---------------------|
| GeoNetwork   | [geonetwork](https://hub.docker.com/_/geonetwork/) | Metadata catalog                   | geonetwork          |
| Nginx        | [nginx](https://hub.docker.com/_/nginx)        | Reverse proxy and web server       | nginx               |
| PostGIS      | [postgis/postgis](https://hub.docker.com/r/postgis/postgis/) | Spatial database                   | database            |
| Elasticsearch| [elasticsearch](https://hub.docker.com/_/elasticsearch) | Search engine                      | elasticsearch       |
| Kibana       | [kibana](https://hub.docker.com/_/kibana)      | Data visualization                 | kibana              |


## Usage

1. Clone this repository.
2. Run `docker compose up` to start all services.
3. Access GeoNetwork at [http://localhost:8080/geonetwork](http://localhost:8080/geonetwork).

Default credentials:
- Username: `admin`
- Password: `admin`

## Update SSL Certificate

To update the local SSL certificate, follow these steps:

1. Generate a new certificate and private key:
  ```sh
  openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout nginx/setup/geonetwork-docker_local.key \
    -out nginx/setup/geonetwork-docker_local.crt \
    -subj "/C=ES/ST=Madrid/L=Madrid/O=Development/CN=localhost"
  ```

2. Verify the files were created:
  ```sh
  ls -l nginx/setup/geonetwork-docker_local.*
  ```

3. Restart the nginx container:
  ```sh
  docker compose restart nginx
  ```

> [!CAUTION]
> This certificate is for local development only. In production, use a valid certificate from a certificate authority.