pipeline {
    agent any
    
    stages {
        stage('Instalar dependencias') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Construyendo el proyecto..."
                    sh 'npm install || true' 
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
