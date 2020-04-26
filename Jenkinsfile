pipeline {
environment{
 registry_blue = "ptrr/capstoneblue"
 registry_green = "ptrr/capstonegreen"
 registryCredential = "e26d40a7-65ed-4a4c-92fe-ac016ab5d94d"
 dockerImage = ""
}
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e blue/*.html'
        sh 'tidy -q -e green/*.html'
      }
    }
    stage('Build Docker Image') {
      steps {
         script {
          dir("blue"){
           dockerImage_blue = docker.build registry_blue
           }
        dir("green"){   
        dockerImage_green = docker.build registry_green
      } 
     }   
    }
   }
   stage('Push Docker Image'){
     steps{
         script {
           docker.withRegistry( '', registryCredential ) {
           dockerImage_blue.push()
           dockerImage_green.push()  
          }
        }
    }
   }
   stage('Deploying') {
       steps{
        withAWS(credentials:'capstone', region: 'eu-central-1'){
      sh "aws eks --region eu-central-1 update-kubeconfig --name capstone3"
       dir("blue"){
      sh "kubectl apply -f ./blue-controller.json"
      }
       dir("green"){
      sh "kubectl apply -f ./green-controller.json"
      }
      sh "kubectl apply -f ./blue-green-service.json"
      sh "kubectl get nodes"
      sh "kubectl get pods" 
       }
      }
     }
   stage('Cleaning up'){
    steps{
       sh "docker rmi $registry_blue"
       sh "docker rmi $registry_green"
   }
  }
 }
}

