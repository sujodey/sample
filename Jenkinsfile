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
	success{
        always {
                emailext attachLog: true,
                body: "${currentBuild.result}: ${BUILD_URL}: Build# ${BUILD_NUMBER}",
                compressLog: true,
                recipientProviders: [[$class: 'DevelopersRecipientProvider'],
                [$class: 'RequesterRecipientProvider']],
                subject: "Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}"
            }
			}
        
	failure {
	sh "echo 'failure'"
		  // Send Failure Email
	 publishHTML target: [
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
