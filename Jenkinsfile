pipeline {
	agent any
	
	stages {
	    

       // Munit testing
      
       stage('Munit Test') {
           steps {
           bat 'mvn clean test '
           }
       }
       // Build the artefact
        stage('artifact package') {
            steps {
                bat ' mvn clean test'
		     // publish html
        publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'reports',
            reportFiles: 'summary.html',
            reportName: 'Munit Report'
          ]
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
