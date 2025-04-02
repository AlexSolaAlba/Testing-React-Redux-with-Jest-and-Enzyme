pipeline {
    agent any
    
    stages {
        stage('Generar hashes SHA-256') {
            steps {
                script {
                    def timestamp = new Date().format("yyyyMMdd_HHmmss")
                    def hashFile = "hashes_${timestamp}.txt"
                    def targetPath = "/var/lib/jenkins/workspace/PipelineBuildTestDeploy/"
                    sh "find ${targetPath} -type f -exec sha256sum {} + > ${hashFile}"
                    archiveArtifacts artifacts: hashFile, fingerprint: true
                }
            }
        }
	}
}

