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
                sh 'cd /home/sysadmin/Documents/react/my-app && pwd'
                sh 'pm2 stop my-app'
            }
        }
    }
    
}
