pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('unittest-image')
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    docker.image('unittest-image').inside('-w /app') {
                        // Commands to run inside the Docker container
                        sh 'ls'
                        sh 'java -jar target/testimage.jar'
                    }
                }
            }
        }
    }
}
