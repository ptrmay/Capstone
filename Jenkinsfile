pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e Docker/*.html'
      }
    }
    stage('Build Docker Image') {
      steps {
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
          sh '''
             cd Docker 
             docker build -t ptrr/cloudcapstone:$BUILD_ID .
          '''
    }
   }
 }
   stage('Push Docker Image'){
     steps{
         withDockerRegistry([ credentialsId: "e26d40a7-65ed-4a4c-92fe-ac016ab5d94d", url: "" ]){
         sh '''
            docker push ptrr/cloudcapstone
         '''
     }
    }
   }
  }
}

