pipeline {
    agent any
    stages {
        stage('Build JAR') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t user-service:1.0 .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker stop user-preprod || true'
                sh 'docker rm user-preprod || true'
                sh 'docker run -d -p 8081:8081 --name user-preprod user-service:1.0'
            }
        }
    }
}