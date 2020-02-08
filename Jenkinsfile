pipeline {
    agent any
	stages{
        stage('Build') {
			agent {
                docker { image 'maven:3-alpine' }
            }
            steps {
               sh 'mvn -B -DskipTests clean package'
			   archiveArtifacts 'target/*.jar'
	   	sh 'mvn sonar:sonar -Dsonar.host.url=http://ec2-34-229-231-15.compute-1.amazonaws.com:9000 -Dsonar.login=a0f02f276fb2a5a25b1865d32e1b5e4d5e53b51a'
            }
	}
    }
}
