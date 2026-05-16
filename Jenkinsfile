pipeline {

    agent any

    environment {
        APP_NAME = "pipeline-python"
        CONTAINER_NAME = "pipeline-container"
    }

    stages {

        stage('Verificar Python') {
            steps {
                sh 'python3 --version'
            }
        }

        stage('Criar Ambiente Virtual') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                '''
            }
        }

        stage('Instalar Dependencias') {
            steps {
                sh '''
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Executar Testes') {
            steps {
                sh '''
                . venv/bin/activate
                pytest
                '''
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