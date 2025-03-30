pipeline {
    agent any
   
    stages {
    
		stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    echo "Instalando dependencias..."
                    sh 'npm install'
                }
            }
        }
        
        stage('Build') {
            steps {
                echo 'Construyendo el proyecto...'
                // Aquí ejecutamos un build, generalmente con un comando como `npm run build`
                sh 'npm run build'
            }
        }
        
        stage('Testing') {
            parallel {
                // Pruebas Unitarias (Jest)
                stage('Unit Tests') {
                    steps {
                        echo 'Ejecutando pruebas unitarias...'
                        // Ejecuta las pruebas unitarias con Jest
                        sh 'npm run test -- --coverage'
                    }
                }
                
                // Pruebas con Enzyme
                stage('Enzyme Tests') {
                    steps {
                        echo 'Ejecutando pruebas con Enzyme...'
                        // Ejecuta las pruebas de Enzyme (esto puede depender de cómo esté configurado el proyecto)
                        sh 'npm run test:enzyme'
                    }
                }
            }
        }

        // Etapa de Deploy (si lo deseas)
        /*stage('Deploy') {
            when {
                branch 1-prueba-rama-feature  // Solo en la rama feature
            }
            steps {
                echo 'Desplegando el proyecto...'
                // Aquí puedes agregar comandos para hacer el deploy si es necesario
                sh 'echo "Despliegue realizado!"'
            }
        }*/
    }

    post {
        always {
            echo 'Este paso siempre se ejecutará al final del pipeline.'
        }
        success {
            echo 'El pipeline se ejecutó con éxito.'
        }
        failure {
            echo 'El pipeline falló.'
        }
    }
}
