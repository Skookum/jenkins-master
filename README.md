# jenkins-master

[![Docker Repository on Quay](https://quay.io/repository/skookum/jenkins/status "Docker Repository on Quay")](https://quay.io/repository/skookum/jenkins)

A Jenkins master Docker image with plugins for running in Kubernetes pre-installed. Based on [jenkinsci/docker](https://github.com/jenkinsci/docker).

## Usage

```bash
docker run -p 8080:8080 -p 50000:50000 quay.io/skookum/jenkins
```
