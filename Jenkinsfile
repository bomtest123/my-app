pipeline {
    tools {nodejs "nodejs"}
    environment {
        CI = 'true'
    }
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3001:3001'
        }
    }

    stages {
        stage('Install package') {
        steps {
            sh "node --version"
            sh "pm2 prettylist"
        }
        }

       
                
        stage('Build') {
        steps {
            echo "Branch is ${env.BRANCH_NAME}..."
            sh "pm2 start my-app-build.json"
        }
        }

        stage('Test') {
        steps {
            sh "pm2 start 'npm test'"
        }
        }
        
        stage('Deploy') {
        steps {
            sh "pm2 start my-app.json"
        }
        }
    }
}
