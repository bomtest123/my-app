pipeline {
    tools {nodejs "nodejs"}
    agent any
    environment {
        CI = 'true'
    }

    stages {
        stage('Install package') {
        agent {
            docker {
                image 'node:lts-bullseye-slim'
                args '-p 3000:3000'
                }
        } 
        steps {
            sh "node --version"
        }
        }
                
        stage('Build') {
        steps {
            sh "pm2 start 'npm run build'"
        }
        }

        stage('Test') {
        steps {
            sh "pm2 start 'npm test'"
        }
        }
        
        stage('Deploy') {
        steps {
            sh "pm2 start 'npm start'"
        }
        }
    }
}
