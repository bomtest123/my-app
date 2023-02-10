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
            script {
                if (fileExists('/home/sysadmin/Documents/react/my-app/my-app.json')) {
                    echo "File src/main/rersources/index.html found!"
                    sh "pm2 start my-app.json"
                }
            }
            
        }
        }
        
        stage('Deploy') {
        steps {
            sh "pm2 start my-app.json"
        }
        }
    }
}

