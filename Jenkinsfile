pipeline {
    agent any
    
    stages {
        stage('Instalar dependencias') {
            steps {
                sh 'npm install --save-dev @babel/preset-env @babel/preset-react babel-jest'
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Construyendo el proyecto..."
                    sh 'npm install --force || true'
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
