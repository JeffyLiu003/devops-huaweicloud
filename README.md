# devops-huaweicloud
DevOps on HuaweiCloud

## 1. Build a docker image based on Jenkins and add libltdl7 library for docker exec
reference the Dockerfile-jenkins-2.150.3.libltdl7, build it and push to SWR.

## 2. Install and config Jenkins
1. Jenins image jenkins-2.150.3.libltdl7
2. Enable privileged container
3. Volume mounts
    - Persistent storage(EVS) mount on /var/jenkins_home
    - Local path /var/run/docker.sock to container path /var/run/docker.sock
    - Local path /usr/bin/docker to container path /usr/bin/docker
4. expose 8080 port to external access
5. Login Jenkins, setup first user, install default plugins
6. Install **Kubernetes Cli** and **(Kubernetes Continuous Deploy)[https://wiki.jenkins.io/display/JENKINS/Kubernetes+Continuous+Deploy+Plugin]** plugin

## 3. Get SWR credential
1. Prepare the SWR credential from [this guide](https://support-intl.huaweicloud.com/usermanual-swr/swr_01_1000.html)
2. summary of the setps:
- got the AK/SK first
- open shell, set ```AK=<your access key>```, ```SK=<your secret key>```
- execute ```printf "$AK" | openssl dgst -binary -sha256 -hmac "$SK" | od -An -vtx1 | sed 's/[ \n]//g' | sed 'N;s/\n//'```, you will get your login key
- replace you information into this command: ```docker login -u [Name of the regional project]@[AK] -p [Login key] [Image repository address]```

## 4. Get CCE credential
1. go to Resource Management -> Cluster Manageent -> Select your destination cluster -> Click More and Kubectl -> On the page click link under "Download the kubectl configuration file"

## 5. Import CCE credential to Jenkins