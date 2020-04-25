pipeline {
  agent any
  stages {
    stage('build cluster') {
      steps {
        sh 'eksctl create cluster \
--name capstone2 \
--region eu-central-1 \
--nodegroup-name standard-workers \
--node-type t3.small \
--nodes 2 \
--nodes-min 1 \
--nodes-max 3 '
      }
    }
  }
}
