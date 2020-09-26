pipeline{
   agent  { label 'jenkinsSlave1' } 
   stages {
       stage("package"){
	        steps {
			    bat 'mvn clean package'
			}
	   }
	  
   }
}
