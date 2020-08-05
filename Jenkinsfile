pipeline {
	agent any
	
	stages {
	   
        // Munit testing
       // stage('MUnit Testing') {
            //steps {
              // sh 'mvn clean test'
	   // }
		
	        
       // }
		stage(' Moving Munit to external folder'){
			steps{
			sh '''
			echo " ${WORKSPACE} "
			cd ${WORKSPACE}
			mkdir MunitReports

                           '''				
			}
		}
	}
	
	post {
		success {
		  sh "echo 'success'"
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
		  sh "echo 'failure'"
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


