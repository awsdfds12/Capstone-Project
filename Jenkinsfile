pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    stages {
        stage('checkout') {
            steps {
                git url:'https://github.com/awsdfds12/Capstone-Project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                // sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                // sh 'npm run test'
                echo "Test"
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t reactimage .'
                sh 'docker tag reactimage:latest krishtonnaik1/dev:latest'
            }
        }
        stage('Docker login') {
            steps {
                 withCredentials([string(credentialsId: 'dock-password', variable: 'dockerHubPassword')]) {
                    sh "${dockerCMD} login -u krishtonnaik1 -p ${dockerHubPassword}"
                    sh "${dockerCMD} push krishtonnaik1/dev:latest"
                }
            }
        }
        stage('Start Docker Service') {
                sh 'sudo service docker start'
        }

    stage('Deploy Docker Container') {
                sh 'sudo docker run -itd -p 8084:8081 krishtonnaik1/dev:latest'
        }
    }
}
