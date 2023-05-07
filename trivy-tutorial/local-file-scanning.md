# Scan local project

At times you might want to scan you locally stored projects for vulnerabilities. This can be done using the `fs` (filesystem) target. So to scan some project you have stored locally the syntax would be: `trivy fs some-path-where-to-scan`. As for the repo target, as per default, Trivy will use the vulnerability and secret scanner if you don't specify otherwise. Lets try it out.

## Create local project

First lets create some local go project.

```
mkdir some-great-name-here && cd some-great-name-here
```{{exec}}

```
go mod init github.com/some-username/some-great-name-here
```{{exec}}

Lets add a dependency that contains a vulnerability.

```
go get gopkg.in/yaml.v2@v2.2.4
```{{exec}}

Although you ideally would want to write some code to use the dependency, we'll skip that now since the dependency is already listed in the project files and that is enough for Trivy. So lets scan our local project. We'll specify the current folder as the path.

```
trivy fs .
```{{exec}}

Great! Now we'll just license the project and be done with it.

```
echo "
The Easter Egg License

The legal power of this license nonexistent. Regardless, this software is licensed under the Easter Egg License, which means that you, in addition to following any other licenses this software is subject to, you must hide an Easter egg somewhere in your code.

If you comply with these criteria, you are free to use, modify, and distribute this software in any way you like. However, if you fail to include an Easter egg in your code, your project will be subject to severe disappointment." > LICENSE
```{{exec}}

## Specifying different scanners

As when scanning repos from previous steps, we could specify different scanners than the defaults that are implied without specifying anything. That would be done by the `--scanners` flag. For example we could specify just secret scanning: `trivy fs --scanners secret .`{{exec}}. No leaked secrets in this project as expected.
