pipeline {
    agent any

    stages {
        stage('Github Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/hongseunghyun123/cicd-test.git'
            }
        }

        stage('Git clone end') {
            steps {
                sh 'touch cicd_test.txt'
                sh 'echo "git clone end" > cicd_test.txt'
            }
        }

        stage('Deploy Server') {
            steps {
                sshagent(credentials: ['Deploy-Privatekey']) {
                    sh '''
                        scp -o StrictHostKeyChecking=no index.html ubuntu@3.38.110.136:/home/ubuntu/
                        ssh -o StrictHostKeyChecking=no ubuntu@3.38.110.136 "sudo mv /home/ubuntu/index.html /var/www/html/index.html"
                    '''
                }
            }
        }
    }
}