pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${env.DOCKER_HUB_USER}/weather-forecast:latest -f src/WeatherForecast.WebApi/Dockerfile ."
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerHubCredentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                        sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                    }
                    sh "docker push ${env.DOCKER_HUB_USER}/weather-forecast:latest"
                }
            }
        }
    }
}
