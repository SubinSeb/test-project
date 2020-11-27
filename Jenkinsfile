pipeline {
  agent any
  stages {
    stage('Build result') {
      steps {
        sh 'sudo docker build -t dockersamples/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'sudo docker build -t dockersamples/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'sudo docker build -t dockersamples/worker ./worker'
      }
    }
    
  }
}
