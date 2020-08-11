pipeline {
	agent any
	
	
	 environment {
		 DEMO = 'http://3.250.224.60:8080/job/Munittest-sampleproject'
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
			FILE="${WORKSPACE}/MunitReports/MunitReport-$BUILD_ID.html"
                       if ( -f  "$FILE" ) then
                       {
                            emailext (
                                to: '${DEFAULT_RECIPIENTS}',
                                subject: "Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}",
                                body: "${DEMO}/${BUILD_NUMBER}/Munit_20Report",
                                attachLog: true,
                            )
                        }
			else 
				{
					echo "muletime error"
				}
                	fi
			
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


