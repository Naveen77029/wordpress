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
                sh 'docker build -t my-wordpress ./'
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                script {
                    // Stop and remove the old container if it exists
                    def oldContainer = sh(script: "docker ps -q -f name=my-wordpress-container", returnStdout: true).trim()
                    if (oldContainer) {
                        echo "Stopping old container: ${oldContainer}"
                        sh "docker stop ${oldContainer}"
                        echo "Removing old container: ${oldContainer}"
                        sh "docker rm ${oldContainer}"
                    } else {
                        echo "No existing container to stop."
                    }
                }
            }
        }

        stage('Deploy New Container') {
            steps {
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
