pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "cool_counters:latest"
    }

    stages {
        stage('Clonar Repositorio') {
            steps {
                git branch: 'main', url: 'https://github.com/JuanMudi/taller-devops-ms.git'            }
        }

        stage('Instalar Dependencias') {
            steps {
                sh 'pip install pylint django --break-system-packages'
            }
        }

        stage('Desplegar Aplicación') {
            steps {
                sh 'cd docker && docker-compose up --build'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completado exitosamente!'
        }
        failure {
            echo 'Pipeline falló. Revisa los logs para más detalles.'
        }
    }
}
