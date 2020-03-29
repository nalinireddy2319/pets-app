pipeline{
   agent any
   
   tools {
      maven 'maven3'
    }
   
   stages{ 
	    stage('Nexus deploy'){
	   	steps{
	   		sh 'mvn clean package'
	   	}
		    stage('Maven Build/Package'){
	   	steps{
	   		nexusArtifactUploader 
			artifacts: [[artifactId: 'pets-app', classifier: '', file: 'target/pets-app.war', type: 'war']], 
			credentialsId: 'nexus3', 
			groupId: 'in.javahome', 
			nexusUrl: '18.191.222.159:8081', 
			nexusVersion: 'nexus3', 
			protocol: 'http', 
			repository: 'pets-app-snapshot', 
			version: '1.0-SNAPSHOT'
	   	}
	   }
   }
}
