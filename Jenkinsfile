pipeline {
  agent any
  environment{
    DOCKER_CONTENT_TRUST=1
    DOCKER_CONTENT_TRUST_SERVER="https://10.1.1.6:443"
  }
  stages {
    stage("Fix the permission issue") {
      steps {
        sh "sudo chown root:jenkins /run/docker.sock"
      }
    }  
    stage('Build result') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh 'sudo docker build -t 10.1.1.6:443/dockersamples/result ./result'
        }  
      }
    } 
    stage('Build vote') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh 'sudo docker build -t 10.1.1.6:443/dockersamples/vote ./vote'
        }  
      }
    }
    stage('Build worker') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/docker-local') {
          sh 'sudo docker build -t 10.1.1.6:443/dockersamples/worker ./worker'
        }  
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/dockersamples') {
          sh 'echo ${26418bc0-b2e4-4a07-9ef1-3643a5289b0e} | sudo -S docker push 10.1.1.6:443/dockersamples/result'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/dockersamples') {
          sh 'echo ${26418bc0-b2e4-4a07-9ef1-3643a5289b0e} | sudo -S docker push 10.1.1.6:443/dockersamples/vote'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443/dockersamples') {
          sh 'echo ${26418bc0-b2e4-4a07-9ef1-3643a5289b0e} | sudo -S docker push 10.1.1.6:443/dockersamples/worker'
        }
      }
    }
  }
}
