pipeline{
   agent  none 
   stages {
       stage("package"){
	       agent { label 'jenkinsSlave1' }
	        steps {
			    bat 'mvn clean package'
			}
	   }
	   stage("install"){
		agent { label 'jenkinsSlave2' }
	        steps {
			    bat 'mvn install'
			}
	   }
	   stage("deploy"){
		agent { label 'jenkinsSlave3' }
	        steps {
			    bat 'mvn deploy'
			}
	   }
	  
   }
}
