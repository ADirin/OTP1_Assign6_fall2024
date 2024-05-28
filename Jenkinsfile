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
                    def app = docker.build("unittest-image")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    def workspaceUnixPath = "${env.WORKSPACE}".replaceAll('\\\\', '/')
                    def app = docker.image("unittest-image")
                    app.inside("-w ${workspaceUnixPath} -v ${workspaceUnixPath}:${workspaceUnixPath} -v ${workspaceUnixPath}@tmp:${workspaceUnixPath}@tmp") {
                        bat 'cmd.exe'
                    }
                }
            }
        }
    }
}
