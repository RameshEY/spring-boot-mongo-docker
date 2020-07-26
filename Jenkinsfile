pipeline {

environment {
     registry = "testdockerramesh/spring-boot-mongo"
     registryCredential = 'dockerhub'
     dockerImage = ''
}
agent {label 'kubetcat'}
	
	
 
  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/RameshEY/spring-boot-mongo-docker.git',branch: 'master'
      }
    }

    stage('Build and Test Application') {
            steps{
               
                sh './mvn clean install'
            }
      }

stage('Building Docker image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    } 
    
	
	stage('Push Docker Image') {
      steps {
          withCredentials([string(credentialsId: 'DOKCER_HUB_PASSWORD', variable: 'DOKCER_HUB_PASSWORD')]) {
          sh "docker login -u testdockerramesh -p ${DOKCER_HUB_PASSWORD}"
        }
        sh 'docker push testdockerramesh/spring-boot-mongo'
         
      }
    }
   

  }

}
