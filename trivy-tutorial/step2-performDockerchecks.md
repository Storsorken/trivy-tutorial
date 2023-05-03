Create a small sample application to build a Docker image.

Create a folder named nginx-image and create a folder named files

`mkdir -p nginx-image/files`{{exec}}

Create a simple HTML file & config file as our app code and package it using Docker.

```
echo -e "
server {\n
    listen 80 default_server;\n
    listen [::]:80 default_server;\n
    root /usr/share/nginx/html;\n
    index index.html index.htm;\n
    server_name _;\n
    location / {\n
        try_files $uri $uri/ =404;\n
    }\n
}\n
" > nginx-image/files/config.txt
```{{exec}}

```
echo -e "
<html>\n
  <head>\n
    <title>Dockerfile</title>\n
  </head>\n
  <body>\n
    <div class='container'>\n
      <h1>My App</h1>\n
      <h2>This is my first app</h2>\n
      <p>Hello everyone, This is running via Docker container</p>\n
    </div>\n
  </body>\n
</html>\n
" > nginx-image/files/index.html
```{{exec}}


Create a Dockerfile in the nginx-image folder

```
echo -e "
FROM ubuntu:18.04  \n
RUN  apt-get -y update && apt-get -y install nginx \n
COPY files/config.txt /etc/nginx/sites-available/config.txt \n
COPY files/index.html /usr/share/nginx/html/index.html \n
EXPOSE 80 \n
CMD ['/usr/sbin/nginx", "-g", "daemon off;'] \n
" > nginx-image/Dockerfile
```{{exec}}

Build Docker image.

`docker build -t nginx:1.0 nginx-image/.`{{exec}}


list the available docker images
`docker images`{{exec}}


Perform Trivy image scan on the built image. After scanning you can observe the report.
`trivy image nginx:1.0`{{exec}}

Perform the Trivy configuration scanning of Dockerfile. 
`trivy config ./nginx-image`{{exec}}
