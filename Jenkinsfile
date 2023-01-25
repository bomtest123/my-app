pipeline {
    tools {nodejs "nodejs"}
    agent any
    environment {
        CI = 'true'
    }

    stages {
        stage('Install package') {
        steps {
            sh "node --version"
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
