## Setup Continous Integration - Jenkins

1. `cd /vagrant/data/jenkins_docker/`
2. `docker build -t viseo/jenkins-docker .`
3. `docker tag viseo/jenkins-docker local.dtr/viseo/jenkins-docker`
4. `docker login local.dtr`
5. user/password is *jenkins/password*
6. `docker push local.dtr/viseo/jenkins-docker`
7. `cd /vagrant`
8. `docker stack deploy --compose-file docker-compose-ci.yml ci`

<!--
## Deploy a custom/specific image to a service

1. `docker service update --image 192.168.88.10:5000/demo-app:1.0.0 demo_web`

## Deploy Service Manually

1. `docker stack deploy --compose-file docker-compose.yml demo`

## Build Demo Web App (Local)

1. `cd /vagrant/data/app`
2. `docker build -t demo-app:1.0.0 .`
3. `docker run -it --rm --name demo-app --network host demo-app:1.0.0`
4. `curl 192.168.88.10:3000`
//5. `docker tag demo-app:1.0.0 192.168.88.10:5000/demo-app:1.0.0`
//6. `docker push 192.168.88.10:5000/demo-app:1.0.0`
-->
