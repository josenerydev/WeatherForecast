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
                    // Construindo a imagem Docker
                    sh "docker build -t ${env.DOCKER_HUB_USER}/weather-forecast:latest src/WeatherForecast/"
                }
            }
        }

        // Opcional: se você tiver testes que possam ser executados em um container
        // stage('Test') {
        //     steps {
        //         script {
        //             // Executando testes no container
        //             sh "docker run ${env.DOCKER_HUB_USER}/seu_projeto:latest dotnet test --logger:trx"
        //         }
        //     }
        // }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Logando no Docker Hub (use credenciais armazenadas de forma segura!)
                    withCredentials([usernamePassword(credentialsId: 'dockerHubCredentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                        sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                    }

                    // Enviando a imagem para o Docker Hub
                    sh "docker push ${env.DOCKER_HUB_USER}/weather-forecast:latest"
                }
            }
        }
    }
}
