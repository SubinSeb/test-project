pipeline {
  agent any
  stages {
    stage("Fix the permission issue") {
      steps {
        sh "sudo su; export DOCKER_CONTENT_TRUST=1; export DOCKER_CONTENT_TRUST_SERVER='https://10.1.1.6:4443'; export DOCKER_CONTENT_TRUST_ROOT_PASSPHRASE='qwerty12345'; export DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE='qwerty12345'; "
      }
    }  
    stage('Build result') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh 'sudo docker build -t 10.1.1.6:443/dockersamples/result:latest ./result'
        }  
      }
    } 
    stage('Build vote') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh 'sudo docker build -t 10.1.1.6:443/dockersamples/vote:latest ./vote'
        }  
      }
    }
    stage('Build worker') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh 'sudo docker build -t 10.1.1.6:443/dockersamples/worker:latest ./worker'
        }  
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/dockersamples') {
          sh '''sudo su
              export DOCKER_CONTENT_TRUST_SERVER='https://10.1.1.6:4443'
              export DOCKER_CONTENT_TRUST_ROOT_PASSPHRASE='qwerty12345' 
              export DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE='qwerty12345'
              docker push 10.1.1.6:443/dockersamples/result:latest --disable-content-trust=0'''
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/dockersamples') {
          sh '''sudo su
              export DOCKER_CONTENT_TRUST_SERVER='https://10.1.1.6:4443'
              export DOCKER_CONTENT_TRUST_ROOT_PASSPHRASE='qwerty12345' 
              export DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE='qwerty12345' 
              docker push 10.1.1.6:443/dockersamples/vote:latest --disable-content-trust=0'''
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/dockersamples') {
          sh '''sudo su
              export DOCKER_CONTENT_TRUST_SERVER='https://10.1.1.6:4443' 
              export DOCKER_CONTENT_TRUST_ROOT_PASSPHRASE='qwerty12345' 
              export DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE='qwerty12345' 
              docker push 10.1.1.6:443/dockersamples/worker:latest --disable-content-trust=0'''
        }
      }
    }
  }
}
