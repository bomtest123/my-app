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
                sh "pm2 prettylist"
                checkout scmGit(
                    branches: [[name: 'master']],
                    userRemoteConfigs: [[url: 'https://github.com/bomtest123/my-app']])
            }
        }
      
        stage('Build') {
            steps {
                echo "Branch is ${env.BRANCH_NAME}..."
                echo "Current directory is ${env.WORKSPACE}"
                sh "pm2 start my-app-build.json"
            }
        }

        stage('Test') {
            steps {
                script {
                    if (fileExists('/home/sysadmin/Documents/react/my-app/my-app.json')) {
                        echo "File my-app.json found!"
                        sh "pm2 start my-app.json"
                    }
                }

            }
        }
        
        stage('Stop Server') {
            steps {
                sh "pm2 stop my-app.json"
            }
        }
    }
}

