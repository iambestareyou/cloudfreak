pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JAVA_HOME'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('iambestareyou/pet_ha', "./docker")
                 docker.withRegistry('https://registry.hub.docker.com', 'dockerlogin') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
