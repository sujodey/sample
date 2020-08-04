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
bat '''  mkdir "C:\\Program Files (x86)\\Jenkins\\workspace\\Munit test- sample project\\MunitReports"
                      move "C:\\Program Files (x86)\\Jenkins\\workspace\\Munit test- sample project\\target\\site\\munit\\coverage\\summary.html"  "C:\\Program Files (x86)\\Jenkins\\workspace\\Munit test- sample project\\MunitReports" 
				ren "C:\\Program Files (x86)\\Jenkins\\workspace\\Munit test- sample project\\MunitReports\\summary.html" "summary-%build_ID%.html" '''				
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
            reportDir: 'C:/Program Files (x86)/Jenkins/workspace/Munit test- sample project/MunitReports',
	    reportFiles: 'summary-${build_ID%.html}',
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
            reportFiles: 'summary-%build_ID%.html',
            reportName: 'Munit Report'
          ]
		}
	}
}


