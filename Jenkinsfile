pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "426281568042.dkr.ecr.us-west-2.amazonaws.com/nginx"
    }
    stages {
        stage('build app') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'ecr:ap-southeast-1:aws-credentials', url: 'https://633799498526.dkr.ecr.ap-southeast-1.amazonaws.com/kalbe-dev') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
