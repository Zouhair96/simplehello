pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage("Maven Build") {
            steps {
                script {
                    bat "mvn clean package"
                }
            }
	}
	stage("Maven deploy") {
            steps {
                script {
                    bat "mvn deploy"
                }
            }
        }
    /*    stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                   nexusArtifactUploader artifacts: [
					   [
						   artifactId: 'Hello',
						   classifier: '',
						   file: 'C:/jenkins/JenkinsHome/workspace/Jenkins_Nexus/target/Hello-1.0-SNAPSHOT.jar',
						   type: 'jar'
					   ]	
				   ],
				   credentialsId: 'admin',
				   groupId: 'org.exemple.demo',
				   nexusUrl: 'localhost:8081',
				   nexusVersion: 'nexus3',
				   protocol: 'http',
				   repository: 'http://localhost:8081/repository/maven-snapshots/',
				   version: '1.0-SNAPSHOT'
                }
            }
        }*/
    }
	 
}
