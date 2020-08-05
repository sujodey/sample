pipeline {
	agent any
	
	stages {
	   
        // Munit testing
        stage('MUnit Testing') {
            steps {
               sh 'mvn clean test'
	    }
		
	        
        }
		stage(' publishing Munit Reports'){
			steps{
			sh '''
			echo " ${WORKSPACE} "
			cd ${WORKSPACE}
			mkdir -p  MunitReports
			echo " ${WORKSPACE} "
                     mv ./target/site/munit/coverage/summary.html ./MunitReports/MunitReport-$BUILD_ID.html
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


