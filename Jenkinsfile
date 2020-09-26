pipeline{
   agent  { label 'jenkinsSlave1' } 
   stages {
       stage("package"){
	        steps {
			    node('jenkinsSlave1') {
			    bat 'mvn clean package'
			}
	   }
	   stage("install"){
	        steps {
			    node('jenkinsSlave2') {
			    bat 'mvn install'
			}
	   }
	   stage("package"){
	        steps {
			    node('jenkinsSlave3') {
			    bat 'mvn deploy'
			}
	   }
	  
   }
}
