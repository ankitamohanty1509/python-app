pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ankitamohanty1509/python-app'  // Change this to your actual DockerHub repo
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Repository already cloned by Jenkins.'
            }
        }

        stage('Package App') {
            steps {
                sh 'zip -r app.zip . -x "*.git*"'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Login & Push to DockerHub') {
            steps {
                withDockerHubRegistry(credentialsId: 'docker-hub-credentials') {
                    sh 'docker push $DOCKER_IMAGE:latest'
                }
            }
        }
    }
}
