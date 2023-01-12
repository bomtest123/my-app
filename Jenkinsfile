pipeline {
  agent any
  environment {
    CI = 'true'
  }
  stages {
    stage('Install package') {
      agent {
        docker { image 'node:16.13.1-alpine' }
      } 
      steps {
        sh 'node --version'
      }
    }
            
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    
    stage('Deploy') {
      steps {
        sh "pm2 start 'ng serve'"
      }
    }
  }
}