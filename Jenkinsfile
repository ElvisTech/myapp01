pipeline {
	agent any

	tools {
		maven "Maven 3.8.6"
	}

	stages {
		stage("Build Artifact") {
			steps {
				sh 'mvn clean package -DskipTests=true'
				archive 'tarjet/*.jar'
			}
		}
		stage ('Test Maven - Junit') {
			steps {
				sh 'mvn test'
			}
			post {
				always {
					junit 'target/surefire-reports/*.xml'
			    	}
			}
		}
		stage ('Sonarqube Analysis - SAST') {
			steps {
				withSonarQubeEnv('SonarQube') {
					sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=my-app -Dsonar.host.url=http://192.168.0.7:9000 -Dsonar.login=sqp_a74f9a9d4de97ec80422e5ede5b966aead9b4125'

				}
			}
		}
	}
}
