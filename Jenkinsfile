pipeline {
	agent any
	
	
	 environment {
		 DEMO = 'http://3.250.224.60:8080/job/Munittest-sampleproject'
		 FILE = '${WORKSPACE}/MunitReports/MunitReport-$BUILD_ID.html'
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
		    if (FILE.exists())
        		echo "file exists"
		    else
                        echo "file does not exists"
	     
}
}
}


