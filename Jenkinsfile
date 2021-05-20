pipeline {
	agent any
	/*{ 
		docker {
			image 'maven:3.6.3' 
			args '-u root:root'
		}
	}*/
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin$PATH"
	}
	stages { 
		stage('Build') {
			steps{
				echo "$PATH"
				sh 'mvn --version'
				sh 'docker version'
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
