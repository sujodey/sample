pipeline {
	agent any
	
	stages {
	    

      
      
        // Munit testing
        stage('MUnit Testing') {
            steps {
                bat ' mvn clean test'
		     // publish html
       
            }
        }
	}
  
	
	post {
		success {
		  bat "echo 'success'"
		  // Send Success Email 
			 publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'coverage',
            reportFiles: 'summary.html',
            reportName: 'Munit Report'
          ]
		}
		failure {
		  bat "echo 'failure'"
		  // Send Failure Email
	   publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'coverage',
            reportFiles: 'summary.html',
            reportName: 'Munit Report'
          ]
		}
	}
}

