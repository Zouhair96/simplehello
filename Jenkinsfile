pipeline{
   agent  none 
   stages {
       stage("package"){
	       agent jenkinsSlave1
	        steps {
			    bat 'mvn clean package'
			}
	   }
	   stage("install"){
		agent jenkinsSlave2
	        steps {
			    bat 'mvn install'
			}
	   }
	   stage("package"){
		agent jenkinsSlave3
	        steps {
			    bat 'mvn deploy'
			}
	   }
	  
   }
}
