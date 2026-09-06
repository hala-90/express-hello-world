pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                sh 'docker build -t express-hello-world-app:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                echo 'Deploying Application...'
                sh 'docker stop express-app-container || true'
                sh 'docker rm express-app-container || true'
                sh 'docker run -d -p 3000:3000 --name express-app-container express-hello-world-app:latest'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully! App is running on port 3000.'
        }
        failure {
            echo 'Pipeline failed. Check the logs.'
        }
    }
}
