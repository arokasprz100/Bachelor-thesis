## Description

This file describes steps needed to setup your own Virtual Machine as a GitLab CI/CD runner. The manual assumes that you have already created your own Virtual Machine with Centos7 as a operating system.

## Manual

### Setting up Docker
This part of manual is based on official Docker documentation.

#### Remove old docker versions

```
sudo yum remove docker \
    docker-client \
    docker-client-latest \
    docker-common \
    docker-latest \
    docker-latest-logrotate \
    docker-logrotate \
    docker-engine
```

#### Install new docker engine and CLI using official repository

##### Install required packages
```
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

##### Set up the repository
```
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

##### Install Docker Engine and CLI
```
sudo yum install docker-ce docker-ce-cli containerd.io
```

##### Start Docker
```
sudo systemctl start docker
```

##### Verify if Docker works properly
```
sudo docker run hello-world
```

### Register virtual machine as a GitLab CI/CD runner
This part of manual is based on official CERN GitLab documentation.

#### Download appropriate packages
```
curl -LJO \
https://gitlab-runner-downloads.s3.amazonaws.com/latest/rpm/gitlab-runner_amd64.rpm
```

#### Install the packages
```
sudo yum install gitlab-runner_amd64.rpm
```

If you want to update runner packages use following command instead:
```
rpm -Uvh gitlab-runner_amd64.rpm
```

#### Download gitlab-runner binary file
```
sudo curl -L --output /usr/local/bin/gitlab-runner \
gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
```

#### Give proper permissions to the binary file
```
sudo chmod +x /usr/local/bin/gitlab-runner
```

#### Create a GitLab CI user
```
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
```

#### Install application and run as a service
```
sudo gitlab-runner install --user=gitlab-runner\
    --working-directory=/home/gitlab-runner
sudo gitlab-runner start
```
<div style="page-break-after: always;"></div>

#### Register the runner

##### Register using gitlab-runner
```
sudo gitlab-runner register
```

##### Enter proper GitLab instance URL
```
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com )
https://gitlab.cern.ch
```

##### Enter token obtained from your GitLab group page > settings > CI/CD > Runners
```
Please enter the gitlab-ci token for this runner
<your_token_here>
```

##### Enter a description for the runner (this can be changed later)
```
Please enter the gitlab-ci description for this runner
[hostname] my-runner
```

##### Enter proper tags (this can be changed later)
```
Please enter the gitlab-ci tags for this runner (comma separated):
ggss-builder
```

##### Enter runner executor
```
Please enter the executor: ssh, docker+machine, docker-ssh+machine,\
kubernetes, docker, parallels, virtualbox, docker-ssh, shell:
docker
```

##### Enter default image (if not defined in .gitlab-ci.yml)
```
Please enter the Docker image (eg. ruby:2.1):
cern/cc7-base:latest
```