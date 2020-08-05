pipeline {
	agent any
	
	stages {
	   
        // Munit testing
        stage('MUnit Testing') {
            steps {
               bat 'mvn clean test'
	    }
		
	        
        }
		stage(' Moving Munit to external folder'){
			steps{
			sh '''
			echo " ${WORKSPACE} "

                           '''				
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
            reportDir: 'MunitReports',
	 reportFiles: 'MunitReport-${build_ID}.html',
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
            reportDir: 'MunitReports',
            reportFiles: 'MunitReport-${build_ID}.html',
            reportName: 'Munit Report'
          ]
		}
	}
}


