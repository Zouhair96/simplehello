pipeline{
   agent  { label 'jenkinsSlave1' } 
   stages {
       stage("package"){
	        steps {
			    bat 'mvn clean package'
			}
	   }
	   stage("install"){
	        steps {
			    bat 'mvn install'
			}
	   }
	   stage("package"){
	        steps {
			    bat 'mvn deploy'
			}
	   }
	  
   }
}
