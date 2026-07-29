pipeline {
    agent any
    stages {
        stage('Build JAR') {
            steps {
                bat 'mvnw.cmd clean package -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t user-service:1.0 .'
            }
        }
        stage('Run Container') {
            steps {
                bat 'docker stop user-preprod || exit 0'
                bat 'docker rm user-preprod || exit 0'
                bat 'docker run -d -p 8081:8081 --name user-preprod user-service:1.0'
            }
        }
    }
}