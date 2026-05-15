pipeline {
    agent any
    stages {
        stage('Verificar Python') {
            steps {
                sh 'python3 --version'
            }
        }
        stage('Executar Aplicacao') {
            steps {
                sh 'python3 app.py'
            }
        }
    }
}
