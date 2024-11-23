pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[
                        credentialsId: 'githubtoken',
                        url: 'https://github.com/TintuMariyamPaul/index.git'
                    ]]
                )
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t my-docker-image:latest .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 3005:80 my-docker-image:latest'
                }
            }
        }
    }
}
