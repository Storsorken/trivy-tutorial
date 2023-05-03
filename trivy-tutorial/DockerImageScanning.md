# Vulnerability scanning for a Official Docker image

Using Trivy we can scan Images on DockerHub for various security issues. Lets start with vulnerability scanning on one of the Docker official image.

By sepcifying simply an image name (and a tag) we can scan for vulnerabilities like.
`$ trivy image [YOUR_IMAGE_NAME]`


We can directly scan the images with out pulling them from the DockerHub.
```
trivy image alpine:3.17.1
```{{exec}}

You can observe that there are 24 vulnerabilities in total in which 10 are HIGH and 14 MEDIUM severity.

We can scan for specific severity vulnerabilities on an Image.
```
trivy image  --severity high alpine:3.17.1
```{{exec}}
