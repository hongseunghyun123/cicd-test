pipeline {
    agent any

    environment {
        strDockerImage = "fgh0830/cicd-test"
    }

    stages {
        stage('Github Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/hongseunghyun123/cicd-test.git'
            }
        }

        stage('Docker image Build') {
            steps {
                script {
                    def oDockImage = docker.build(strDockerImage, "-f Dockerfile .")
                }
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