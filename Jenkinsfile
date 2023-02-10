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
           dir('/var/lib/jenkins/workspace/my-app_master'){
                sh "pm2 stop my-app"
                //sh "rm application_snapshot-001.jar"
                checkout scmGit(
                    branches: [[name: 'master']],
                    userRemoteConfigs: [[url: 'https://github.com/bomtest123/my-app']])
                //sh "mv path/to/new/jar path/to/old/jar application_snapshot-001.jar"
                //sh "pm2 start start-switch.JSON"
            }
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

