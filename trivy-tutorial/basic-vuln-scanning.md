# Vulnerability scanning for project on GitHub

Using Trivy we can scan projects on GitHub for various security issues (some other platforms are also supported, see docs). Lets start with vulnerability scanning.

## Basic vulnerability scanning

When doing vulnerability scanning Trivy will check the projects dependencies against databases for known vulnerabilities of the used version.
Lets try it out.

Suppose we are considering to use or maybe build upon an open-source tool called [go-git](https://github.com/go-git/go-git). Lets use Trivys vulnerability scanner to check for any known vulnerabilities.

We could explicitly specify the vulnerability scanner like this: `trivy repo --scanners vuln https://github.com/go-git/go-git`. However, by default, when scanning repositories using `trivy repo url-to-git-repo` it is equivalent to `trivy repo --scanners vuln, secret url-to-git-repo`. So we can just use:

```
trivy repo https://github.com/go-git/go-git
```{{exec}}


Do you see any vulnerabilities? Since things might have changed only you can tell. 

### Check out specific commit

Lets check out a commit we know has a vulnerability

```
trivy repo --commit 02856b824a05c18118c116af5b0e2bca1b3496b3 https://github.com/go-git/go-git
```{{exec}}

Here we see that they use a package called gopkg.in/yaml.v2, but their current version has a known vulnerability. We see that there is a version of that package where that issue has been fixed. The issue seems to be of medium severity. We can also checkout a provided link for more info on the vulnerability [https://avd.aquasec.com/nvd/cve-2019-11254](https://avd.aquasec.com/nvd/cve-2019-11254). 

### Check out specific tag

We can checkout specific tags. Maybe we are using an older version, or are considering to use an older version due to, for example, compatibility issues. 

```
trivy repo --tag v.5.4.1 https://github.com/go-git/go-git
```{{exec}}

Oh, maybe we should consider upgrading if possible.

### Check out specific branch

To checkout a specific branch use `--branch <branch name here>`.

```
trivy repo --branch exact-sha1 https://github.com/go-git/go-git
```{{exec}}
