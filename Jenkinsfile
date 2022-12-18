pipeline {
    
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'start install
                sh 'npm install'
                echo 'installed'
            }
        }
        stage('Test') {
            steps {
                echo 'start test'
                sh 'npm test'
                echo 'test succeeded'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def app = docker.build("my-node-app:${env.BUILD_ID}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', Zidecaido1: 'DOCKER_HUB_PASSWORD', PieterJanDelie: 'DOCKER_HUB_USERNAME')]) {
                    sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                    sh "docker push my-node-app:1"
                }
            }
        }
    }
}
