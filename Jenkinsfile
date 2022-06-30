//scripted

//declarative
pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				echo "Build"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	} post {
		always {
			echo "run always"
		}
		success {
			echo "run when successful"
		}
		failure {
			echo "run when fail"
		}
	}
}
