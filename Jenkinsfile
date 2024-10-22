pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = '51b2b76f-1fcf-4a56-a6ef-488ff1461489' // Your Docker Hub credentials ID
        DOCKER_IMAGE_NAME = 'naveen687/wordpress-custom' // Custom image name
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Cloning your public GitHub repository
                git 'https://github.com/Naveen77029/wordpress.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t ${DOCKER_IMAGE_NAME} .'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        // Automatic login
                    }
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Push the image to Docker Hub
                    sh 'docker push ${DOCKER_IMAGE_NAME}'
                }
            }
        }

        stage('Deploy Using Docker') {
            steps {
                script {
                    // Stop the old container if running
                    sh 'docker stop my-wordpress-container || true'
                    sh 'docker rm my-wordpress-container || true'

                    // Run the new container on port 8081
                    sh 'docker run -d -p 8081:80 --name my-wordpress-container ${DOCKER_IMAGE_NAME}'
                }
            }
        }
    }

    post {
        always {
            // Archive artifacts if needed
            archiveArtifacts artifacts: '**/*.html', onlyIfSuccessful: true
        }
    }
}
