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
                echo "workspace is ${env.WORKSPACE}..."
                sh "cd /var/www/my-repository/source && pwd"
                sh "pm2 stop my-app"
            }
        }
    }
    
}
