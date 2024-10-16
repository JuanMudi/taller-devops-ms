pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "cool_counters:latest"
    }

    stages {
        stage('Clonar Repositorio') {
            steps {
                git 'https://github.com/deparkes/simple-django-app.git'
            }
        }

        stage('Instalar Dependencias') {
            steps {
                sh 'pip install pylint'
            }
        }

        stage('Ejecutar Pylint') {
            steps {
                sh '''
                    FILES=$(find . -name "*.py")
                    if [ -z "$FILES" ]; then
                        echo "No se encontraron archivos Python para analizar."
                        exit 1
                    fi
                    pylint $FILES
                '''
            }
        }

        stage('Desplegar Aplicación') {
            steps {
                sh 'cd docker && docker-compose up -d'
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
