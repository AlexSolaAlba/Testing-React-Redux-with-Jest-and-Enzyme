pipeline {
    agent any
    
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
                sh 'npx jest --coverage --passWithNoTests --config=jest.config.js'
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
