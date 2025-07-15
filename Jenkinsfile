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
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t logistics-tracker .'
            }
        }

        stage('Start with Docker Compose') {
            steps {
                sh 'docker-compose down || true'
                sh 'docker-compose up -d --build'
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
