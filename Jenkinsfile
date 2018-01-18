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
			xldCreatePackage  artifactsPath: 'target\test-project-1.0.war', darPath: "test-project-1.0.dar", manifestPath: "deployit-manifest.xml"
		}
    }
	
}
