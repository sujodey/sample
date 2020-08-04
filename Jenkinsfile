pipeline {
	agent any
	
	stages {
	   
        // Munit testing
        stage('MUnit Testing') {
            steps {
                bat ' mvn clean test' }
		
	        
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
            reportDir: 'Jenkins/jobs/Munit test- sample project/builds/*.*/htmlreports/Munit_20Report',
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
            reportDir: 'Jenkins/jobs/Munit test- sample project/builds/*.*/htmlreports/Munit_20Report',
            reportFiles: 'summary.html',
            reportName: 'Munit Report'
          ]
		}
	}
}

