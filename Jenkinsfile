pipeline {
  agent any
  sh "sudo chown root:jenkins /run/docker.sock"
  stages {
    stage('Build result') {
      steps {
        sh 'sudo docker build -t 10.1.1.6:443/dockersamples/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'sudo docker build -t 10.1.1.6:443/dockersamples/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'sudo docker build -t 10.1.1.6:443/dockersamples/worker ./worker'
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443') {
          sh 'sudo docker push 10.1.1.6:443/dockersamples/result'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443') {
          sh 'sudo docker push 10.1.1.6:443/dockersamples/vote'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: '2d946ebb-4b0c-4a32-8756-f115273f9f61', url:'https://10.1.1.6:443') {
          sh 'sudo docker push 10.1.1.6:443/dockersamples/worker'
        }
      }
    }
  }
}
