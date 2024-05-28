pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("unittest-image")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    docker.image("unittest-image").inside {
                        sh 'java -jar /app/testimage.jar'
                    }
                }
            }
        }
    }
}
