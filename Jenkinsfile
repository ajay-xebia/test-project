pipeline{
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
		stage('Build'){
             steps {
                echo "Building solution"  
                script {
					def mavenbuild = tool name: 'maven3'
                    bat "${mavenbuild}/bin/mvn package"
                }                 
             }
        }
		stage('Package & Publish'){
			steps{
				nexusArtifactUploader artifacts: [[artifactId: 'test-project', classifier: '', file: 'target/test-project-1.0.war', type: 'war']], credentialsId: '506fc323-c597-454a-8c8b-be845b6a23d1', groupId: 'com.pipeline', nexusUrl: '192.168.56.103:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: '1.0'
				xldCreatePackage  artifactsPath: 'target', darPath: "test-project-1.0.dar", manifestPath: "deployit-manifest.xml"
				xldPublishPackage darPath: "test-project-1.0.dar", serverCredentials: "admin-credentials"
				
			}
		}
    }
	
}
