pipeline {

agent {label 'kubetcat'}
	
	environment {
        //be sure to replace "ianp5uk" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "testdockerramesh/spring-boot-mongo
    }
 
  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/RameshEY/spring-boot-mongo-docker.git',branch: 'master'
      }
    }

  
	
    stage('Build Docker Image') {
      steps {
          app = docker.build(DOCKER_IMAGE_NAME)
         
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
