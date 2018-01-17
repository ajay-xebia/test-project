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
                    bat "${mavenbuild}/maven build test-project"
                }                 
             }
        }
    }
	
}
