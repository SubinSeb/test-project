pipeline {
  agent any
  stages {
    stage("Fix the permission issue") {
      steps {
        sh ""
      }
    }  
    stage('Build result') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh '''sudo su
              docker build -t 10.1.1.6:443/dockersamples/comp_result:latest ./result --disable-content-trust=0'''
        }  
      }
    } 
    stage('Build vote') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh '''sudo su
             docker build -t 10.1.1.6:443/dockersamples/comp_vote:latest ./vote --disable-content-trust=0'''
        }  
      }
    }
    stage('Build worker') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh '''sudo su
              docker build -t 10.1.1.6:443/dockersamples/comp_worker:latest ./worker --disable-content-trust=0'''
        }  
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/dockersamples') {
          sh '''sudo su
              export DOCKER_CONTENT_TRUST_SERVER='https://10.1.1.6:4443'
              export DOCKER_CONTENT_TRUST_ROOT_PASSPHRASE=$fbc9c4e4-eac7-417e-b3c4-c4b1005386db
              export DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE=$fbc9c4e4-eac7-417e-b3c4-c4b1005386db
              docker push 10.1.1.6:443/dockersamples/comp_result:latest --disable-content-trust=0'''
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
              docker push 10.1.1.6:443/dockersamples/comp_vote:latest --disable-content-trust=0'''
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
              docker push 10.1.1.6:443/dockersamples/comp_worker:latest --disable-content-trust=0'''
        }
      }
    }
  }
}
