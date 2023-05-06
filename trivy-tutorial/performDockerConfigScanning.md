# Docker configuration scanning using Trivy
Trivy can be used to scan Dockerfiles, Kubernetes manifests, and Helm charts for container configuration files. This can help in the investigation of security flaws or misconfigurations in the container image build process.

Following command can be used to scan the Dockerfile.
 `trivy config <path-to-dockerfile>`

## Creating sample appliction
Create a sample application to build a Docker image for scanning.
Make a HTML file that will be used to show a static website and package it using Docker.

```
mkdir -p nginx-image/files
```{{exec}}

```
echo -e "
<html>\n
  <head>\n
    <title>Trivy-Tutorial</title>\n
  </head>\n
  <body>\n
    <div class='docker_container'>\n
      <h1>A simple Application</h1>\n
      <h2>This is a sample application</h2>\n
      <p>Hello everyone, This is running via Docker container</p>\n
    </div>\n
  </body>\n
</html>\n
" > nginx-image/files/index.html
```{{exec}}

## Create and build a Dockerfile
Create a Dockerfile in the nginx-image folder.
```
echo -e "
FROM ubuntu:18.04  \n
RUN  apt-get -y update && apt-get -y install nginx \n
COPY files/index.html /usr/share/nginx/html/index.html \n
EXPOSE 80 \n
CMD ['/usr/sbin/nginx", "-g", "daemon off;'] \n
" > nginx-image/Dockerfile
```{{exec}}

Build Docker image and check if everything works as per the configuration.

```
docker build -t nginx_trivy:1.0 nginx-image/.
```{{exec}}

List the available docker images and see if the image is built succesfully.
```
docker images
```{{exec}}

## Scan Docker image for vulnerabilities
Perform Trivy image scan on the built image. After scanning you can observe the report.
```
trivy image nginx_trivy:1.0
```{{exec}}

## Perform Docker configuration scanning
Perform the Trivy configuration scanning of Dockerfile.
This will scan the Dockerfile and its associated base image, and report any vulnerabilities found.
```
trivy config ./nginx-image
```{{exec}}
