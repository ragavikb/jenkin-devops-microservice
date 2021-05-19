pipeline {
	agent { docker {image 'maven:3.6.3'} args '-u root:root'}
	stages { 
		stage('Build') {
			steps{
				echo "mvn --version"
				echo "Build"
			}
		
		}	
		stage('Test') {
			steps{
				echo "Test"
			}
		
		}
		stage('Integration Test') {
			steps{
				echo "Integration Test"
			}
		
		}
	} 
	post {
		always {
			echo 'Awesome. I run always'
		}
		success {
			echo 'I run when successfull'
		}
		failure {
			echo 'I run when failure'
		}
	}
	
}
