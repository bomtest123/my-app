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
        sh 'npm run build'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    
    stage('Deploy') {
      steps {
        sh "pm2 start 'npm start' &"
      }
    }
  }
}