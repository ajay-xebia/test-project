pipeline{
    agent any
	environment {
		mavenBuildTool = 'maven3'
		GROUP_ID='com.pipeline'
		PROJECT_NAME = 'test-project'
		PROJECT_VERSION='1.0'
		NEXUS_URL='192.168.56.103:8081/nexus'
		NEXUS_REPO='releases'
		
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
				nexusArtifactUploader artifacts: [[artifactId: '${PROJECT_NAME}', classifier: '', file: 'target/${PROJECT_NAME}-${PROJECT_VERSION}.war', type: 'war']], credentialsId: '506fc323-c597-454a-8c8b-be845b6a23d1', groupId: '${GROUP_ID}', nexusUrl: '${NEXUS_URL}', nexusVersion: '${NEXUS_REPO}', protocol: 'http', repository: 'releases', version: '${PROJECT_VERSION}'
				xldCreatePackage  artifactsPath: 'target', darPath: "${PROJECT_NAME}-${PROJECT_VERSION}.dar", manifestPath: "deployit-manifest.xml"
				xldPublishPackage darPath: "${PROJECT_NAME}-${PROJECT_VERSION}.dar", serverCredentials: "admin-credentials"
				
			}
		}
    }
	
}
