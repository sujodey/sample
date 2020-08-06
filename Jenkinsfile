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
			mv "${WORKSPACE}"/target/site/munit/coverage/summary.html "${WORKSPACE}"/MunitReports/MunitReport-$BUILD_ID.html
                    
                           '''				
			}
		}
	}
	
	
	post {
        always {
		
               emailext attachLog: true, body: " <h1>Build Result</h1> <h2> ${currentBuild.result}:</h2>  <h3> Please find the MUnit&Integration test Results from Below link</h3> <h2>http://54.194.63.35:8080/job/Munittest-sampleproject/${BUILD_ID}/Munit_20Report/</h2>", compressLog: true, replyTo: 'satheesh.chitti@capgemini.com',
       subject: "Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}", to: 'sandhya.a.n@capgemini.com,sreedhar.butta@capgemini.com' 
	
			
	 publishHTML  target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'MunitReports',
            reportFiles: 'MunitReport-${BUILD_ID}.html',
            reportName: 'Munit Report'
          ]
		
}
}
}


