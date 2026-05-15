pipeline {
    agent any
    stages {
        stage('Clonar Repositorio') {
            steps {
                git 'https://github.com/MysteryNySory/Pipeline-Python-Jenkins.git'
            }
        }
        stage('Verificar Python') {
            steps {
                sh 'python --version || python3 --version'
            }
        }
        stage('Executar Aplicacao') {
            steps {
                sh 'python app.py || python3 app.py'
            }
        }
    }
}
