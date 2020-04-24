pipeline {
environment{
 registry = "ptrr/capstone"
 registryCredential = "e26d40a7-65ed-4a4c-92fe-ac016ab5d94d"
 dockerImage = ""
}
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }
    stage('Build Docker Image') {
      steps {
         script {
           dockerImage = docker.build registry + ":$BUILD_NUMBER"
      }   
    }
   }
   stage('Push Docker Image'){
     steps{
         script {
           docker.withRegistry( '', registryCredential ) {
           dockerImage.push()
            }
        }
    }
   }
   stage('Deploying') {
      sh "aws eks --region eu-central-1 update-kubeconfig --name capstone1"
      }
   stage('Cleaning up'){
    steps{
       sh "docker rmi $registry:$BUILD_NUMBER"
   }
  }
 }
}

