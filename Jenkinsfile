pipeline{
    agent any
	environment {
		mavenBuildTool = 'maven3'
	}
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
					def mavenbuild = tool name: mavenBuildTool
                    bat "${mavenbuild}/bin/mvn package"
                }                 
             }
        }
		stage('Package & Publish'){
			steps{
				nexusArtifactUploader artifacts: [[artifactId: 'test-project', classifier: '', file: 'target/test-project-${BUILD_NUMBER}.war', type: 'war']], credentialsId: '506fc323-c597-454a-8c8b-be845b6a23d1', groupId: 'com.pipeline', nexusUrl: '192.168.56.103:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: '${BUILD_NUMBER}'
				xldCreatePackage  artifactsPath: 'target', darPath: "test-project-${BUILD_NUMBER}.dar", manifestPath: "deployit-manifest.xml"
				xldPublishPackage darPath: "test-project-${BUILD_NUMBER}.dar", serverCredentials: "admin-credentials"
				
			}
		}
    }
	
}
