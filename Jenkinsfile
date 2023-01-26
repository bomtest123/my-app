pipeline {
    tools {nodejs "nodejs"}
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
            def workspace = pwd()
            echo "Branch is ${env.BRANCH_NAME}..."
            echo "Current directory is ${workspace}"
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

