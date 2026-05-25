pipeline {
    agent any

   

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from version control...'
                checkout scm
            }
        }

        stage('Build & Test Backend') {
            steps {
                echo 'Installing Backend Dependencies...'
                dir('server') {
                    bat 'npm install'
                }
            }
        }

        stage('Build & Test Frontend') {
            steps {
                echo 'Installing Frontend Dependencies & Building...'
                dir('client') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                echo 'Building Docker Images...'
                bat 'docker compose build'
            }
        }

        stage('Deploy Containers') {
            steps {
                echo 'Deploying application using Docker Compose...'
                bat 'docker compose up -d'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully! All containers are running.'
        }
        failure {
            echo 'Pipeline failed! Please check the logs.'
        }
    }
}
