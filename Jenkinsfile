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
                sh 'pip install pylint --break-system-packages'
            }
        }

        stage('Ejecutar Pylint') {
            steps {
                sh '''
                    FILES=$(find . -name "*.py" -not -name "__init__.py")
                    if [ -z "$FILES" ]; then
                        echo "No se encontraron archivos Python para analizar."
                        exit 1
                    fi
                    pylint $FILES --errors-only
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
