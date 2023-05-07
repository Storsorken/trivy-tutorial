# Odds and ends about Trivy and its vulnerability scanning

## More functionality

There is much more functionality to Trivy than we could cover in this tutorial. So if you found this interesting, feel free to check out the documentation for more functionality. Also read:

```
trivy help
```{{exec}}

If you are wondering why there is no repo command it is because repo is an alias for the repository command.

## Still under development

As of writing this tutorial the Trivy tool is still under development. As of now, the tool functions better for some languages than others. Go seems to have the best support. So we would advice you to study the documentation for your use case.

## How dependency vulnerability scanning works

The way Trivy checks for dependency vulnerabilities is by looking for project files that list the dependencies and their versions for the project and then checks those against different databases of known vulnerabilites.
