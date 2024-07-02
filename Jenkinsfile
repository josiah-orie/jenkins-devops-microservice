pipeline {
	// agent any
	//agent { docker{ image 'maven:3.9.8'} } //for using docker image
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build') {
			steps{
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
