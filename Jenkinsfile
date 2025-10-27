pipeline {
    agent any

    environment {
        IMAGE_NAME = "nodejs-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('clone'){
            steps{
                git branch: 'main', url: 'https://github.com/ahmedglala/senior-repo'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo ' Building Docker image...'
                sh """
                    docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                """
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running Docker container...'
                script {
                    // Stop old container if it exists
                    sh "docker rm -f ${IMAGE_NAME} || true"

                    // Run the container
                    sh """
                        docker run -d -p 3000:3000 --name ${IMAGE_NAME} ${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
        }
    }

}
