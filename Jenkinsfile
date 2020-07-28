pipeline {
	agent any
	
	stages {
	    

      
      // Build the artefact
        stage('package') {
            steps {
                bat 'mvn clean package'
            }
        }
        // Munit testing
        stage('MUnit Testing') {
            steps {
                bat 'mvn test'
            }
        }
	}
  
	
	post {
		success {
		  bat "echo 'success'"
		  // Send Success Email 
		}
		failure {
		  bat "echo 'failure'"
		  // Send Failure Email 
		}
	}
}
