pipeline {
    agent any 

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the Git repository
                git 'https://github.com/Naveen77029/wordpress.git'
            }
        }

        stage('Build') {
            steps {
                // You can add specific build commands if necessary
                echo 'Building the project...'
                // For example, you might run a build script or a specific command
                // sh './build.sh' // Uncomment and modify as needed
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                echo 'Building Docker image...'
                sh 'docker build -t my-wordpress ./'
            }
        }

        stage('Test Docker Access') {
            steps {
                // Test Docker access
                echo 'Testing Docker access...'
                sh 'docker ps'
            }
        }

        stage('Test Docker Image') {
            steps {
                // Run tests (if any)
                echo 'Running tests...'
                // Replace with actual test commands if needed
                // Example: sh 'docker run my-wordpress test-command'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the Docker container on port 8081
                echo 'Deploying Docker container...'
                sh 'docker run -d -p 8081:80 my-wordpress'
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
