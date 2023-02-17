  def remote = [:]
    remote.name = 'test'
    remote.host = '10.33.2.106'
    remote.user = 'sysadmin'
    remote.password = 'admin123'
    remote.allowAnyHosts = true

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
                sshCommand remote: remote, command: "cd " + pathDir
                sshCommand remote: remote, command: "pm2 l"
            }
        }
        stage('Checkout Application source code') {
            steps {
                checkout scmGit(
                    branches: [[name: 'master']],
                    userRemoteConfigs: [[url: 'https://github.com/bomtest123/my-app']],)
            }
        }
        stage('Stop remote node') {
            steps {
                sshCommand remote: remote, command: "cd " + pathDir
                sshCommand remote: remote, command: "pm2 stop my-app"
                
            }
        }
        stage('Delete files from remote node') {
            steps {
                sshRemove remote: remote, path: pathDir + "/test.sh"
                sshCommand remote: remote, command: 'rm my-app/*.jar', failOnError:'false'
            }
        }
        stage('Move files to remote node') {
            steps {
                sshPut remote: remote, from: 'test2.sh', into: pathDir + '/test2.sh'
            }
        }

        stage('Deploy RuPay Switch') {
            steps {
                   sshCommand remote: remote, command: 'pm2 start my-app.json', failOnError:'false'
               
            }
        }
    }
}
