 def remote = [:]
    remote.name = 'test'
    remote.host = '10.33.2.103'
    remote.user = 'sysadmin'
    remote.password = 'admin123'
    remote.allowAnyHosts = true

def remote1 = [:]
    remote1.name = 'test1'
    remote1.host = '10.33.2.104'
    remote1.user = 'sysadmin'
    remote1.password = 'admin123'
    remote1.allowAnyHosts = true

def remote2 = [:]
    remote2.name = 'test2'
    remote2.host = '10.33.2.105'
    remote2.user = 'sysadmin'
    remote2.password = 'admin123'
    remote2.allowAnyHosts = true

def pathDir = "/home/sysadmin/Documents/Tests/my-app"


pipeline {
    tools {nodejs "nodejs"}
    agent any
    environment {
        CI = 'true'
    }

    stages {
        stage('Check server status') {
            steps {
                sshCommand remote: remote, command: "pm2 l"
                sshCommand remote: remote1, command: "pm2 l"
                sshCommand remote: remote2, command: "pm2 l"
            }
        }
        stage('Checkout Application files') {
            steps {
                checkout scmGit(
                    branches: [[name: 'dev']],
                    userRemoteConfigs: [[url: 'https://github.com/bomtest123/my-app']],)
            }
        }
        
        stage('Stop Server') {
            steps {
                sshCommand remote: remote, command:"cd " +pathDir+ "; sudo ./my-app.sh"
                sshCommand remote: remote1, command:"cd " +pathDir+ "; sudo ./my-app.sh"
                sshCommand remote: remote2, command:"cd " +pathDir+ "; sudo ./my-app.sh"
                sshCommand remote: remote, command: "pm2 stop APP_NAME"
                sshCommand remote: remote1, command: "pm2 stop APP_NAME"
                sshCommand remote: remote2, command: "pm2 stop APP_NAME"
                sshRemove remote: remote, path: pathDir + "/test.sh"
              
            }
        }
      
        stage('Move files to remote node') {
            steps {
                sshCommand remote: remote, command: 'rm my-app/*.jar', failOnError:'false'
                sshPut remote: remote, from: 'application_snapshot-001.jar', into: pathDir + '/application_snapshot-001.jar'
            }, 
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
    }
}

