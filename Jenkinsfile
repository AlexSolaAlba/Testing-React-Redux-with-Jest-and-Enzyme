pipeline {
    agent any
    
    environment {
        // Usamos node.js para este proyecto React/Redux
        NVM_DIR = "/home/alumno/.nvm"
        PATH = "/home/alumno/.nvm/versions/node/v18.20.7/bin:$PATH"
    }

    stages {
        // Etapa de Build
        stage('Build') {
            steps {
                echo 'Construyendo el proyecto...'
                // Aquí ejecutamos un build, generalmente con un comando como `npm run build`
                sh '''
                chmod +x /home/alumno/.nvm/versions/node/v18.20.7/bin/npm
                npm run build
            '''
            }
        }

        // Etapa de Testing
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
        stage('Deploy') {
            when {
                branch 1-prueba-rama-feature  // Solo en la rama feature
            }
            steps {
                echo 'Desplegando el proyecto...'
                // Aquí puedes agregar comandos para hacer el deploy si es necesario
                sh 'echo "Despliegue realizado!"'
            }
        }
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
