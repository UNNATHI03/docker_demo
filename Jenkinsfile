pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "unnathi03/myapp:v1"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/UNNATHI03/docker_demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp .'
            }
        }

        stage('Tag Image') {
            steps {
                bat 'docker tag myapp %DOCKER_IMAGE%'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat '''
                    echo %PASS% | docker login -u %USER% --password-stdin
                    docker push %DOCKER_IMAGE%
                    '''
                }
            }
        }
    }
}