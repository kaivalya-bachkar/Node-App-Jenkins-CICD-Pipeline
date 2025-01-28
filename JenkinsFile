pipeline {
    agent any
    tools{
        nodejs 'mynode'
    }
    environment {
        SSH_CREDENTIALS = 'ubuntu'
        REMOTE_USER = 'ubuntu'
        REMOTE_SERVER = '13.203.75.242'
    }

    stages {
        stage('Git Cloning ') {
            steps {
                echo 'Hello World'
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kaivalya-bachkar/Node-App-Jenkins-CICD-Pipeline.git']])
            }
        }
        stage('Build') {
            steps {
                echo 'Building a Nodeapp'
                sh "npm install"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                sh "./node_modules/mocha/bin/_mocha --exit ./test/test.js"
            }
        }
        stage('Deploy') {
            steps {
                sshagent(credentials: [SSH_CREDENTIALS]) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no $REMOTE_USER@$REMOTE_SERVER << EOF
                            cd /home/ubuntu/node1/
                            git pull https://github.com/kaivalya-bachkar/Node-App-Jenkins-CICD-Pipeline.git
                            npm install
                            npm run
                            sudo npm install -g pm2
                            npm audit fix --force
                            pm2 start index.js
                            exit
                            EOF
                    '''
                }
            }
        }
    }
}
