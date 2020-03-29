pipeline{
   agent any
   
   tools {
      maven 'maven3'
    }
   
   stages{
	   
	    stage('Maven Build/Package'){
			steps{
				sh 'mvn clean package'
			}
	   }
	   
	   stage('Nexus Deploy'){
			steps{
				nexusArtifactUploader artifacts: [[artifactId: 'pets-app', classifier: '', file: 'target/pets-app.war', type: 'war']], 
				credentialsId: 'nexus3', 
				groupId: 'in.javahome', 
				nexusUrl: '18.191.222.159:8081', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'pets-app-snapshot', 
				version: '1.0-SNAPSHOT'
			}
	   }
	   
	    stage('DEPLOYE WAR FILE TO TOMCAT'){
			steps{
				sshagent(['tomcat-dev']) {
					sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.20.8:/opt/tomcat8/webapps/pets-app.war"
					
					sh "ssh ec2-user@172.31.20.8 /opt/tomcat8/bin/shutdown.sh"
					
					sh "ssh ec2-user@172.31.20.8 /opt/tomcat8/bin/startup.sh"
				}
			}
	   }
   }
}
