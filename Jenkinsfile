pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Obteniendo codigo del repositorio proyecto-ci-poli...'
                checkout scm
            }
        }

        stage('Validar Node.js y dependencias') {
            steps {
                sh 'node -v && npm -v'
                sh 'npm install --no-audit --no-fund'
                sh 'node --check index.js'
            }
        }

        stage('Validar configuracion Docker') {
            steps {
                sh 'docker compose config -q'
                echo 'Configuracion de contenedores verificada correctamente.'
            }
        }
    }

    post {
        success {
            echo 'Pipeline de integracion continua completado con exito.'
        }
        failure {
            echo 'Error en alguna etapa del pipeline.'
        }
    }
}
