pipeline {
	agent any
	// agent { docker{ image 'maven:3.6.3'} } for using docker image
	stages{
		stage('Build') {
			steps{
				sh 'mvn --version'
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
