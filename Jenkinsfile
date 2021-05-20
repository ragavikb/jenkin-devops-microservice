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
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages { 
		stage('Checkout') {
			steps{
				echo "$PATH"
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
			}
		
		}
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}	
		stage('Test') {
			steps{
				sh "mvn test"
			}
		
		}
		stage('Integration Test') {
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		
		}
		stage ('Package'){
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image'){
			steps {
				//docker build -t ragavikb/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage = docker.build("agavikb/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps {
				script{
					docker.withRegistry('', 'dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
					
				}
				
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
