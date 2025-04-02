pipeline {
    agent any
    
    stages {
        stage('Obtener versiones') {
            steps {
                script {
                    def timestamp = new Date().format("yyyyMMdd_HHmmss")
                    def versionFile = "versiones_${timestamp}.txt"
                    sh "java -version 2>&1 | tee ${versionFile}"
                    sh "jenkins --version >> ${versionFile}"
                    archiveArtifacts artifacts: versionFile, fingerprint: true
                }
            }
        }
    }
}

