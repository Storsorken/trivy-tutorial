# Vulnerability scanning for private repository on GitHub
To scan private GitHub or GitLab repositories using Trivy, you will need to provide Trivy with credentials to access the repository. Set the environment variable GITHUB TOKEN or GITLAB TOKEN with a valid token having access to the private repository being scanned to access the repository.

Since the GITHUB TOKEN environment variable takes priority over the GITLAB TOKEN environment variable, GITHUB TOKEN must be unset if a private GitLab repository is to be scanned.

### Scanning of private repository with out access rights.
Before setting the GITHUB TOKEN environment variable let's try scanning the repository and check how it behaviours.

```
trivy repo https://github.com/Suvarchala1995/DevOpsDemo
```{{exec}}

You can observe that there is an authorization error from the Trivy.
 
### Adding the GitHub access token of the repository and scan again
Lets now add the GITHUB TOKEN and try the scanning again. 

```
export GITHUB_TOKEN=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
```{{exec}}

Now we added the token as an environment variable, perform the Trivy scanning again.

```
trivy repo https://github.com/Suvarchala1995/DevOpsDemo
```{{exec}}

### Fetch report in json format
Trivy supports different types of report generations like Table, Json, template, sarif, cyclonedx, spdx etc. Default format of the report is Table. we can specify the type of report using --format option. Json format gives more insights of the reports, lets see how it looks.
```
trivy repo --format json https://github.com/Suvarchala1995/DevOpsDemo
```{{exec}}