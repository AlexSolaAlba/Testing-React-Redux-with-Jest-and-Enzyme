pipeline {
    agent any
    
    stages {
        stage('Escanear puertos abiertos') {
            steps {
                script {
                    def timestamp = new Date().format("yyyyMMdd_HHmmss")
                    def scanFile = "puertos_${timestamp}.txt"
                    def ip = sh(script: """hostname -I | awk '{print \$1}'""", returnStdout: true).trim()
                    sh "nmap -p- ${ip} > ${scanFile}"
                    archiveArtifacts artifacts: scanFile, fingerprint: true
                }
            }
        }
	}
}

