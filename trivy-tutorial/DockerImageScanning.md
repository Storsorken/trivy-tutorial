# Vulnerability scanning for an Official Docker image
Trivy is simple to use and can be incorporated into a continuous integration and delivery (CI/CD) pipeline to scan container images as part of the build and deployment process. Trivy compares the contents of a container image to known vulnerabilities and generates a report identifying any vulnerabilities that are discovered. It can read images in a variety of formats, including Docker images, OCI images, and Kubernetes YAML files.

Trivy can scan images at many phases of the container lifecycle, such as development, testing, and production. Developers may detect vulnerabilities early in the development process and avoid security concerns in production by adding Trivy into the CI/CD pipeline.

Using Trivy we can scan Images on DockerHub for various security issues without pulling the image. Lets start with vulnerability scanning on one of the Docker official image. This will be helpful to identify security vulnerabilities in Docker base images before integrating in to the applications.

By sepcifying simply an image name (and a tag) we can scan for vulnerabilities like.
`$ trivy image [YOUR_IMAGE_NAME]`

## Docker image scanning
We can directly scan the images with out pulling them from the DockerHub.
```
trivy image alpine:3.17.1
```{{exec}}

### Scan based on severity
You can observe that there are 24 vulnerabilities in total in which 10 are HIGH and 14 MEDIUM severity.

We can scan for specific severity vulnerabilities on an Image using --severity flag. 
```
trivy image --severity high alpine:3.17.1
```{{exec}}
