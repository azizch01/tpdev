pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'nesrinesaid/tp3express'  
    }

    stages {
        stage('clone code') {
            steps {
                git 'https://github.com/nesrinesaid/Tp3Express.git'
            }
        }
        stage('build') {
            steps {
                script {
                  docker.build("${DOCKER_IMAGE}:1.0")
                }
            }
        }

        stage('push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHubLogin') {
                        docker.image("${DOCKER_IMAGE}:1.0").push()
                    }
                }
            }
        }
    stage('deploy') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHubLogin') {
                        def docker_image = docker.image("${DOCKER_IMAGE}:1.0")
                        docker_image.run('--name tp3express -p 5000:5000')
                 }
                }
            }
        }
    }
}