pipeline {

environment {
     registry = "testdockerramesh/spring-boot-mongo"
     registryCredential = 'dockerhub'
     dockerImage = ''
}
agent any
	
	
 
  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/RameshEY/spring-boot-mongo-docker.git',branch: 'master'
      }
    }

    

stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "springBootMongo.yml", kubeconfigId: "mykubeconfig")
        }
      }
    }
	
	
   

  }

}
