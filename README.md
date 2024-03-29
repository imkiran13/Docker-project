# DOCKER PROJECT

## Docker Installation and Setup


yum install docker -y
systemctl start docker
systemctl status docker


##Dockerfile

FROM ubuntu
RUN apt-get update -y
RUN apt-get install apache2 -y
COPY index.html /var/www/html/
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]

##Docker Concepts
Docker File: To create image by automation.
Docker Compose: To create multiple containers on single server.
Docker Swarm: To create multiple containers on Multiple server.
Docker Stack: Docker swarm + Docker compose

##Cluster Setup

yum install docker -y
systemctl start docker
systemctl status docker
docker swarm init --advertise-addr 172.31.85.110
docker node ls

##Jenkins Installation (Master)

sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
amazon-linux-extras install java-openjdk11 -y 
yum install git maven jenkins -y
systemctl start jenkins.service
systemctl status jenkins.service


##Dockerfile


FROM ubuntu
RUN apt-get update -y
RUN apt-get install apache2 -y
COPY index.html /var/www/html/
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]

Index.html

##Jenkins Pipeline

pipeline {
    agent any 
    
    stages {
        stage('checkout') {
            steps {
              git 'https://github.com/imkiran13/Docker-project.git'
            }
        }
        stage('build') {
            steps {
                sh 'docker build -t $img .'
            }
        }
        stage('tag') {
            steps {
                sh 'docker tag $img $repo'
            }
        }
        stage('push') {
            steps {
                sh 'docker login -u $username -p $password '
                sh 'docker push $repo'
            }
        }
    }
}
##Permissions

chmod 777 /var/run/docker.sock
systemctl daemon-reload
systemctl restart docker.service

##Docker Compose File
yaml
Copy code
version: '3'
services:
  devops:
    image: imkiran13/devopsreponit:latest
    ports:
      - "80:80"
    volumes:
      - "devopsvol"
    deploy:
      replicas: 3

  aws:
    image: imkiran13/awsreponit:latest
    ports:
      - "81:80"
    volumes:
      - "awsvol"
    deploy:
      replicas: 3

  datascience:
    image: imkiran13/datasciencereponit:latest
    ports:
      - "82:80"
    volumes:
      - "datasciencevol"
    deploy:
      replicas: 3

  azure:
    image: imkiran13/azurereponit:latest
    ports:
      - "83:80"
    volumes:
      - "azurevol"
    deploy:
      replicas: 3
