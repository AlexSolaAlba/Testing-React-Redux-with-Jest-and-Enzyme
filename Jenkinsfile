pipeline {
    agent any
    
    environment {
        // Aquí puedes definir variables de entorno globales
        // Ejemplo: NPM_HOME = '/path/to/npm'
    }

    stages {
        stage('Instalar dependencias') {
            steps {
                sh 'npm install --force || true'
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Construyendo el proyecto..."
                    sh 'npm run build --force || true' 
                }
            }
        }
        
        stage('Ejecutar pruebas y generar cobertura') {
            steps {
                sh 'npx jest --coverage --passWithNoTests'
            }
        }

        stage('Publicar reporte de cobertura') {
            steps {
                publishHTML([
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage/lcov-report',
                    reportFiles: 'index.html',
                    reportName: 'Cobertura de Código'
                ])
            }
        }
    }

    post {
        always {
            echo "Pipeline completado."
        }
        
        success {
            echo "El pipeline se completó con éxito."
        }

        failure {
            echo "El pipeline falló."
        }
    }
}
