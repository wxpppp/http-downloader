[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/LinuxSuRen/http-downloader)
[![](https://goreportcard.com/badge/linuxsuren/http-downloader)](https://goreportcard.com/report/linuxsuren/github-go)
[![](http://img.shields.io/badge/godoc-reference-5272B4.svg?style=flat-square)](https://godoc.org/github.com/linuxsuren/http-downloader)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/7cc20ea84e0543068c320e471bde560e)](https://www.codacy.com/gh/LinuxSuRen/http-downloader/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=LinuxSuRen/http-downloader&amp;utm_campaign=Badge_Grade)
[![Codacy Badge](https://app.codacy.com/project/badge/Coverage/7cc20ea84e0543068c320e471bde560e)](https://www.codacy.com/gh/LinuxSuRen/http-downloader/dashboard?utm_source=github.com&utm_medium=referral&utm_content=LinuxSuRen/http-downloader&utm_campaign=Badge_Coverage)
[![codecov](https://codecov.io/gh/LinuxSuRen/http-downloader/branch/master/graph/badge.svg?token=Ntc8z2iEQ2)](https://codecov.io/gh/LinuxSuRen/http-downloader)
[![Contributors](https://img.shields.io/github/contributors/linuxsuren/http-downloader.svg)](https://github.com/linuxsuren/github-go/graphs/contributors)
[![GitHub release](https://img.shields.io/github/release/linuxsuren/http-downloader.svg?label=release)](https://github.com/linuxsuren/github-go/releases/latest)
![GitHub All Releases](https://img.shields.io/github/downloads/linuxsuren/http-downloader/total)
[![LinuxSuRen/open-source-best-practice](https://img.shields.io/static/v1?label=OSBP&message=%E5%BC%80%E6%BA%90%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5&color=blue)](https://github.com/LinuxSuRen/open-source-best-practice)

# Get started
`hd` is a HTTP download tool.

Install it via: `brew install linuxsuren/linuxsuren/hd`

Or download it directly (for Linux):
```
curl https://linuxsuren.github.io/tools/install.sh|sh
```

Or download it via proxy:
```
curl -L https://ghproxy.com/https://github.com/linuxsuren/http-downloader/releases/latest/download/hd-linux-amd64.tar.gz | tar xzv hd
mv hd /usr/bin/hd
```

for Windows users (you might need to add this program into the Windows Defence exclude list):
```
winget install 'HTTP downloader'
```

Want to go through the code? [GitPod](https://gitpod.io/#https://github.com/linuxsuren/http-downloader) definitely can help you.

# Usage

## Download
```shell
hd get https://github.com/jenkins-zh/jenkins-cli/releases/latest/download/mde-linux-amd64.tar.gz --thread 6
```

Or use a simple way instead of typing the whole URL:

```shell
hd get mde
```

Or you might want to download a pre-released binary package from GitHub:

```shell
hd get --pre ks
```

## Install
You can also install a package from GitHub:

```shell
#!title: Install mde with specific threads
hd install mde -t 6
```

or install by a category name:

```shell
hd install --category security
```

## Search
hd can download or install via the format of `$org/$repo`. If you find that it's not working. It might because of there's 
no record in [hd-home](https://github.com/LinuxSuRen/hd-home). You're welcome to help us to maintain it.

When you first run it, please init via: `hd fetch`

then you can search it by a keyword: `hd search jenkins`

## Use multi-stage builds
Do you want to download tools in the Docker builds? It's pretty easy. Please see the following example:

```dockerfile
FROM ghcr.io/linuxsuren/hd:v0.0.42 as downloader
RUN hd install kubesphere-sigs/ks@v0.0.50

FROM alpine:3.10
COPY --from=downloader /usr/local/bin/ks /usr/local/bin/ks
CMD ["ks"]
```

## As a library
You can import it from `github.com/linuxsuren/http-downloader/pkg/installer`, then put the following code to your CLI. 
It can help you to download desired tools:

```go
is := installer.Installer{
    Provider: "github",
}
if err = is.CheckDepAndInstall(map[string]string{
    "ks": "linuxsuren/ks",
    "kk": "kubekey",
}); err != nil {
    return
}
```

## Install other services
It supports to install other services, for example: `bitbucket`.

```shell
hd install bitbucket
```

# Features
* go library for HTTP
* multi-thread
* continuously (TODO)
* GitHub release asset friendly

## Release

This project can be released via [linuxsuren-versions](https://github.com/linuxsuren/linuxsuren-versions).

![Visitor Count](https://profile-counter.glitch.me/{http-downloader}/count.svg)
