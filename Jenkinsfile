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
  }
}
