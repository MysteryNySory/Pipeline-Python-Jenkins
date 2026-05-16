pipeline {

    agent any

    environment {
        APP_NAME = "pipeline-python"
        CONTAINER_NAME = "pipeline-container"
    }

    stages {

        stage('Clonar Repositorio') {
            steps {
                git 'https://github.com/MysteryNySory/Pipeline-Python-Jenkins.git'
            }
        }

        stage('Verificar Python') {
            steps {
                sh 'python3 --version'
            }
        }

        stage('Instalar Dependencias') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Executar Testes') {
            steps {
                sh 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $APP_NAME .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true

                docker run -d \
                    --name $CONTAINER_NAME \
                    -p 5000:5000 \
                    $APP_NAME
                '''
            }
        }
    }

    post {

        success {
            echo 'Deploy realizado com sucesso!'
        }

        failure {
            echo 'Pipeline falhou!'
        }
    }
}