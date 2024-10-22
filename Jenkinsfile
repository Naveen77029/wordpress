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

        stage('Deploy') {
            steps {
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
