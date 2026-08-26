pipeline {
	agent any
	
	environment {
		IMAGE_NAME = "team_skeleton"
	}
	stages {
		stage('Checkout') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
			steps {
				sh "docker build -t ${IMAGE_NAME}:0.1.0 ."
			}
		}
		stage('Test') {
			steps {
				sh "mvn -B test"
			}
			post {
				always {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
	}
	post {
		failure {
			echo "Build failed"
		}
		success {
			echo "Build passed"
		}
	}
}
