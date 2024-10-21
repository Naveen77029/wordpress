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
                    // Build Docker image with the tag 'naveen687'
                    sh 'docker build -t naveen687 .'
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
                    sh 'docker run -d -p 8081:80 --name my-nginx-container naveen687'
                }
            }
        }

        stage('Test Docker Container') {
            steps {
                script {
                    // Wait for the container to start
                    sleep 10

                    // Test the application running in the container
                    def response = sh(script: 'curl -s -o /dev/null -w "%{http_code}" http://localhost:8081/test.html', returnStdout: true).trim()
                    if (response != '200') {
                        error "Application is not running as expected. HTTP response code: ${response}"
                    }
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
