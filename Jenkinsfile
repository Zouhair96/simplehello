pipeline {
    agent any
    tools {
        maven "Maven"
    }
	
    environment {
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "localhost:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "maven-snapshots"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "admin"
    }
    stages {
        stage("Maven Build") {
            steps {
                script {
                    bat "mvn clean package"
                }
            }
	}
	/*stage("Maven deploy") {
            steps {
                script {
                    bat "mvn  deploy"
                }
            }
        }*/
       /* stage("Publish to Nexus Repository Manager") {
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
	    
	    stage("publish to nexus") {
            steps {
                script {
                    // Read POM xml file using 'readMavenPom' step , this step 'readMavenPom' is included in: https://plugins.jenkins.io/pipeline-utility-steps
                    pom = readMavenPom file: "pom.xml";
                    // Find built artifact under target folder
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    // Print some info from the artifact found
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    // Extract the path from the File found
                    artifactPath = filesByGlob[0].path;
                    // Assign to a boolean response verifying If the artifact name exists
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                // Artifact generated such as .jar, .ear and .war files.
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                // Lets upload the pom.xml file for additional information for Transitive dependencies
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
	    stage ('deploy to tomcat'){
   		echo 'deployment started'
       		bat '''copy C:\\jenkins\\JenkinsHome\\workspace\\MavenJenkinsTomcat\\target\\target\\*.war C:\\jenkins\\tomcat\\apache-tomcat-8.5.58-windows-x64\\apache-tomcat-8.5.58\\webapps'''
   }
    }
	 
}
