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
				//sh "mvn test"
			}
		}
		stage('Package') {
			steps{
				echo "Packaging the app..."
				sh "mvn package -DskipTests"
			}
		}
		stage('Integration Test') {
			steps{
				echo "Integration Test..."
		//		sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage("Build Docker Image"){
			steps{
				// "docker build -t jossy10/currency-exchange-devops:$env.BUILD.TAG"
				script{
					dockerImage = docker.build("jossy10/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage("Push Docker Image"){
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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
