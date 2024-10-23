pipeline { 
    agent any 

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Naveen77029/wordpress.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t my-wordpress ./'
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                script {
                    // Find the existing container
                    def oldContainer = sh(script: "docker ps -aq -f name=my-wordpress-container", returnStdout: true).trim()
                    if (oldContainer) {
                        echo "Stopping old container: ${oldContainer}"
                        sh "docker stop ${oldContainer} || true" // Ignore if stop fails
                        echo "Removing old container: ${oldContainer}"
                        sh "docker rm ${oldContainer} || true" // Ignore if remove fails
                    } else {
                        echo "No existing container to stop."
                    }
                }
            }
        }

        stage('Deploy New Container') {
            steps {
                echo 'Deploying new Docker container...'
                sh 'docker run -d --name my-wordpress-container -p 8081:80 my-wordpress'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
