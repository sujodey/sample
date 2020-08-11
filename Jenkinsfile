pipeline {
	agent any
	
	
	 environment {
		 DEMO = 'http://3.250.224.60:8080/job/Munittest-sampleproject'
		 FILE="${DEMO}/${BUILD_NUMBER}/Munit_20Report"
		 
    }
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
			mv "${WORKSPACE}"/target/site/munit/coverage/summary.html "${WORKSPACE}"/MunitReports/MunitReport-$BUILD_ID.html
                    
                           '''				
			}
		}
	}
	
post {
	  always {
		script {
			if FILE.exists then
                       {
		emailext attachLog: true, body: '<h4>Build Result</h4> <h3> ${currentBuild.result}:</h3>  <h4> Please find the MUnit&Integration test Results from Below link</h4> <h3>${DEMO}/${BUILD_NUMBER}/Munit_20Report</h3> <h3>${DEMO}/${BUILD_NUMBER}/Integration_20Test_20Report</h3>', compressLog: true, replyTo: 'sandhya.a.n@capgemini.com', subject: 'Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}', to: 'sandhya.a.n@capgemini.com'
			
	    	publishHTML target: [
            	allowMissing: false,
            	alwaysLinkToLastBuild: false,
            	keepAll: true,
            	reportDir: 'MunitReports',
			reportFiles: 'MunitReport-${BUILD_ID}.html',
            	reportName: 'Munit Report'
            	]
		       }
		else 
				{
					echo "muletime error"
				}
			fi	
		}
	  }
}
}



