pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Cloning your GitHub repository
                git 'https://github.com/Naveen77029/wordpress.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image with the tag 'my-nginx-site'
                    sh 'docker build -t my-nginx-site .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop the old container if running
                    sh 'docker stop my-nginx-container || true'
                    sh 'docker rm my-nginx-container || true'

                    // Run the new container on port 8081
                    sh 'docker run -d -p 8081:80 --name my-nginx-container my-nginx-site'
                }
            }
        }
    }

    post {
        always {
            // Archive the HTML file for reference in Jenkins
            archiveArtifacts artifacts: 'index.html', onlyIfSuccessful: true
        }
    }
}
