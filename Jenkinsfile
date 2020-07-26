pipeline {

  agent {label 'kubetcat'}
  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/MithunTechnologiesDevOps/spring-boot-mongo-docker.git',branch: 'master'
      }
    }

   stage('Maven Clean Package') {
      steps {
         def mavenHome =  tool name: "Maven-3.6.1", type: "maven"
         def mavenCMD = "${mavenHome}/bin/mvn"
         sh "${mavenCMD} clean package"
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
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "springBootMongo.yml, kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
