pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Sughosh28/tracking_parcel.git'
            }
        }

        stage('Build App') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t logistics-tracker .'
            }
        }

        stage('Start with Docker Compose') {
            steps {
                bat 'docker-compose down || true'
                bat 'docker-compose up -d --build'
            }
        }
    }

    post {
        success {
            echo '🚚 Local app deployed successfully using Docker Compose!'
        }
        failure {
            echo '💥 CI/CD failed! Check logs!'
        }
    }
}
