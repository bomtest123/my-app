 def remote = [:]
    remote.name = 'test'
    remote.host = '10.33.2.103'
    remote.user = 'sysadmin'
    remote.password = 'admin123'
    remote.allowAnyHosts = true

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
        
        stage('Remote SSH') {
            steps {
                sshCommand remote: remote, command: "ls -lrt"
                sshCommand remote: remote, command: "for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done"
             
                //sshRemove remote: remote, path: "/home/sysadmin/Documents/Tests/test.sh"
                sshScript remote:remote, script:"/home/sysadmin/Documents/Tests/my-app/my-app.sh"
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

