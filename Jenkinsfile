pipeline{
   agent any
   
   tools {
      maven 'maven3'
    }
   
   stages{
	   stage('GIT CHECKOUT'){
	   	steps{
	   		git credentialsId: 'git', url: 'https://github.com/nalinireddy2319/pets-app'
	   	}
	   }
	   
	    stage('Maven Build/Package'){
	   	steps{
	   		sh 'mvn clean package'
	   	}
	   }
   }
}