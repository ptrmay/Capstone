pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'eksctl create cluster \
--name capstone \
--region eu-central-1 \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \'
      }
    }
  }
}
