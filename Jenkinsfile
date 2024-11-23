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
        stage('Deploy Docker Container') {
            steps {
                script {
                    // Stop and remove the existing container if it exists
                    sh '''
                    if [ $(docker ps -aq -f name=html-application) ]; then
                        docker stop html-container
                        docker rm html-container
                    fi
                    '''
                    // Run a new container with the updated image
                    sh 'docker run -d -p 3008:80 --name html-container my-docker-image:latest'
                }
            }
        }
    }
}
