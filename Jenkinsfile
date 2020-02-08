pipeline {
    agent any

    stages {
	stage('Sonarqube') {
    	    environment {
        	scannerHome = tool 'SonarQubeScanner'
    	}
    	steps {
            withSonarQubeEnv('sonarqube') {
            	sh "${scannerHome}/bin/sonar-scanner"
            }
            timeout(time: 10, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
       }
    }
        stage('Build') {
			agent {
                docker { image 'maven:3-alpine' }
            }
            steps {
               sh 'mvn -B -DskipTests clean package'
			   archiveArtifacts 'target/*.jar'
            }
        }
    }
}
