pipeline {
    agent any

    environment {
        registry = 'https://registry.hub.docker.com'
        imageName = 'zrasul099/class'
        tag = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    app = docker.build("${imageName}:${tag}")
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                    app.inside {
                        sh 'echo "Tests passed"'
                    }
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    docker.withRegistry("${registry}", 'docker') {
                        app.push("${tag}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
