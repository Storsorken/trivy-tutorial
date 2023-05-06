# Continued: Vulnerability scanning for project on GitHub

## Secrets scanning

We don't want to accidentally leak credentials in our projects. Trivy can help with this. By default, when doing a repo scan, Trivy scans for dependency vulnerabilities and leaked secrets. Lets see how Trivy would react to leaked secrets:

```
trivy repo --commit c7dfecb1053e27e79b50c88a7b443f0e1a2c15f8 https://github.com/nginxinc/NGINX-Demos
```{{exec}}

## License scanning

Sometimes you might be considering to use/build upon a specific open-source tool. Then you might first want to know what licenses the project is subject to. Trivy can scan the source code for licenses using its license scanner.

```
trivy repo --scanners license --license-full https://github.com/go-git/go-git
```{{exec}}

Word of caution. The --license-full flag makes the scan more thorough. In our experiments, without that flag many licenses seem to easily be missed.

Note: now we only scanned for licenses. If you want to scan for e.g. vulnerabilites as well in the same scan you would use: `--scanners license,vuln`.
