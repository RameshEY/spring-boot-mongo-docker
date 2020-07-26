pipeline {

agent {label 'kubetcat'}
 
  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/RameshEY/spring-boot-mongo-docker.git',branch: 'master'
      }
    }

  
	
    stage('Build Docker Image') {
      steps {
          sh 'docker build -t testdockerramesh/spring-boot-mongo .'
         
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
