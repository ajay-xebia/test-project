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
					bat set
                    def mavenbuild = tool name: 'maven3'
                    bat "${mavenbuild}/bin/mvn package"
                }                 
             }
        }
		
    }
	
}
