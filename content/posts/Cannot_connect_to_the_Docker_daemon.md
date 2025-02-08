+++
title = 'Cannot connect to the Docker daemon'
date = 2025-02-08T16:21:05+08:00
categories = ["DevOps"]
tags = ["Docker", "GitLab CI/CD", "Kubernetes"]
author=  "Abner Zhou"
draft = false
+++

## 错误复现

参考官网文档配置`.gitlab-ci.yaml`文件内容如下[^1]：

```yaml
default:
  image: docker:24.0.5
  services:
    - name: docker:24.0.5-dind
  before_script:
    - docker info
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY

variables:
  DOCKER_REGISTRY: ${CI_REGISTRY}
  DOCKER_IMAGE: ${CI_REGISTRY_IMAGE}

stages:
  - build

build:
  stage: build
  script:
    - docker build -t $DOCKER_IMAGE:$CI_COMMIT_SHA .
    - docker push $DOCKER_IMAGE:$CI_COMMIT_SHA
    - |
      if [ "$CI_COMMIT_BRANCH" == "main" ]; then
        docker tag $DOCKER_IMAGE:$CI_COMMIT_SHA $DOCKER_IMAGE:latest
        docker push $DOCKER_IMAGE:latest
      fi
```

执行过程中会提示如下错误：

```shell
ERROR: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

## 使用TCP连接并禁用TLS

当使用`dind`服务的时候，必须使用tcp连接，而非sock连接[^2]

> When using dind service, you must instruct docker to talk with the daemon started inside of the service. The daemon is available with a network connection instead of the default `/var/run/docker.sock` socket.

修改yaml文件中的`variables`部分

```yaml
variables:
  DOCKER_HOST: tcp://docker:2375
  # This instructs Docker not to start over TLS.
  DOCKER_TLS_CERTDIR: ""
```

发现错误变成了下面这样

```shell
docker: Cannot connect to the Docker daemon at tcp://docker:2375. Is the docker daemon running?
```

## 等待Docker daemon启动

当使用[Kubernetes executor](https://docs.gitlab.com/runner/executors/kubernetes/index.html#using-dockerdind)时，会遇到Docker daemon还没启动，就尝试连接情况[^3]。

解决方案有两个：

### docker info 循环

增加一个循环，直到docker info能够正常输出以后再进行后续操作

```yaml
before_script:
  - until docker info; do sleep 1; done
  - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
```

### HEALTHCHECK TCP PORT

在设置service的时候，增加一个`HEALTHCHECK_TCP_PORT`操作

```yaml
services:
    - name: docker:dind
      command: [ "--tls=false" ]
      variables:
        HEALTHCHECK_TCP_PORT: "2375"
```

## 完整的gitlab-ci.yaml文件

```yaml
default:
  image: docker:24.0.5
  services:
    - name: docker:24.0.5-dind
      variables:
        HEALTHCHECK_TCP_PORT: "2375"  # 检查2375端口监听情况
  before_script:
    - docker info
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY


variables:
  DOCKER_TLS_CERTDIR: ""   # 禁用TLS
  DOCKER_REGISTRY: ${CI_REGISTRY}
  DOCKER_IMAGE: ${CI_REGISTRY_IMAGE}
  DOCKER_HOST: tcp://docker:2375  # 使用TCP连接

stages:
  - build

build:
  stage: build
  script:
    - docker build -t $DOCKER_IMAGE:$CI_COMMIT_SHA .
    - docker push $DOCKER_IMAGE:$CI_COMMIT_SHA
    - |
      if [ "$CI_COMMIT_BRANCH" == "main" ]; then
        docker tag $DOCKER_IMAGE:$CI_COMMIT_SHA $DOCKER_IMAGE:latest
        docker push $DOCKER_IMAGE:latest
      fi
```

## References

[^1]: [use-docker-in-docker-with-privileged-mode](https://docs.gitlab.com/runner/executors/docker.html#use-docker-in-docker-with-privileged-mode)

[^2]: [Use Docker to build Docker images | GitLab](https://docs.gitlab.com/ee/ci/docker/using_docker_build.html)

[^3]: [Create readiness probes for services in kubernetes executor (#27215) · Issues · GitLab.org / gitlab-runner · GitLab](https://gitlab.com/gitlab-org/gitlab-runner/-/issues/27215)
