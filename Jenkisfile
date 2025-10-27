pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git clone git@github.com:ahmedglala/senior-repo.git
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                docker build -t jenkis-pipe .
            }
        }

        stage('Run Container') {
            steps {
		docker rm -f my-app-container || true
                docker run -d --name my-app-container -p 8080:8080 jenkis-pipe

                script {
                    // Stops old container if exists
                    sh '''
                        docker rm -f my-app-container || true
                        docker run -d --name my-app-container -p 8080:8080 jenkis-pipe
                    '''
                }
            }
        }
    }
}

