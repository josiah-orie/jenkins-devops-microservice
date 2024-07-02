pipeline {
	agent any
	//agent { docker{ image 'maven:3.9.8'} } //for using docker image
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout') {
			steps{
				sh 'mvn --version'
				sh 'docker version'
				sh 'docker images'
				echo "Build"
			}
		}
		stage("Compile"){
			steps{
				echo "compiling..."
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps{
				echo "Initiating Test..."
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps{
				echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	}
	post{
		always{
			echo 'I am awesome. I run always'
		}
		success{
			echo 'I run on success'
		}
		failure{
			echo 'I run on failure'
		}
		// unstable{}: when test fails 
		// changed{} when build status changes
	}
}
