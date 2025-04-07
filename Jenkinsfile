pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ankitamohanty1509/python-app'  // Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                // You can replace this with your actual checkout logic if necessary
                echo 'Repository already cloned by Jenkins.'
            }
        }

        stage('Package App') {
            steps {
                // Create a zip package of the app, excluding the .git directory
                sh 'zip -r app.zip . -x "*.git*"'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Login & Push to DockerHub') {
            steps {
                // Log in to Docker Hub and push the image
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $DOCKER_IMAGE:latest'
                }
            }
        }
    }

    post {
        success {
            echo "Docker image successfully built and pushed to Docker Hub!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
