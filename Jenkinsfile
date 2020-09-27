pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage("Maven Build") {
            steps {
                script {
                    sh "mvn clean package"
                }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                   nexusArtifactUploader artifacts: [
					   [
						   artifactId: 'Hello',
						   classifier: '',
						   file: 'target/Hello1.0-SNAPSHOT.jar',
						   type: 'jar'
					   ]	
				   ],
				   credentialsId: 'admin',
				   groupId: 'org.exemple.demo',
				   nexusUrl: 'localhost:8081',
				   nexusVersion: 'nexus3',
				   protocol: 'http',
				   repository: 'http://localhost:8081/repository/maven-nexus-repo/',
				   version: '1.0-SNAPSHOT'
                }
            }
        }
    }
}
