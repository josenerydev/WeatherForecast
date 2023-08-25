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
                    sh 'docker build -t josenerydev/weather-forecast:latest .'
                }
            }
        }

        // // Opcional: se você tiver testes que possam ser executados em um container
        // stage('Test') {
        //     steps {
        //         script {
        //             // Executando testes no container
        //             sh 'docker run seu_nome_no_dockerhub/seu_projeto:latest dotnet test --logger:trx'
        //         }
        //     }
        // }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Logando no Docker Hub (use credenciais armazenadas de forma segura!)
                    withCredentials([usernamePassword(credentialsId: 'dockerHubCredentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                        sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'
                    }

                    // Enviando a imagem para o Docker Hub
                    sh 'docker push josenerydev/weather-forecast:latest'
                }
            }
        }
    }
}
