pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$Path"
	}
	stages {
		stage('Checkout') {
			steps {
			    sh "mvn --version"
				sh "docker version"
				echo "Build"
				echo "Path $PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "BUILD ID - $env.BUILD_ID"
			}
		}
		stage('Compile') {
			steps {
			    sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package') {
			steps {
				sh "mvn package -D skipTests"
			}
		}

		stage('Build Docker Image') {
			steps {
				//sh "docker build -t jenniecontainer/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("jenniecontainer/jenkin-test:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('','dockerhub') {
						dockerImage.push();
						dockerImage.push('latest')
					}
				}
			}
		}
	} 
	post {
		always {
			echo "always"
		}
		success {
			echo "success"
		}
		failure {
			echo "failure"
		}
	}
}
