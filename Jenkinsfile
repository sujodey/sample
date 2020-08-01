pipeline {
	agent any
	
	stages {
	    

       // Munit testing
      
       stage('Munit Test') {
           steps {
           bat 'mvn clean test '
           }
       }
     
	post {
		success {
		  bat "echo 'success'"
		  // Send Success Email
			   // publish html
        publishHTML target: [
            allowMissing: true,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: '${application.path}/target/site/munit/coverage/*',
            reportFiles: 'summary.html',
            reportName: 'Munit Report'
          ]
		}
		failure {
		  bat "echo 'failure'"
		  // Send Failure Email 
		}
	}
}
