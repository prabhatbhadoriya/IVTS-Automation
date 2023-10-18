pipeline {
  agent {
    node {
      label 'SlaveNode'
    }

  }
  stages {
    stage('test') {
      steps {
        script {
          def scriptOutput = sh 'aws eks list-clusters'
          echo "Shell Script Output: ${scriptOutput}"
          def connect = sh 'aws eks update-kubeconfig --name monitoring-poc'
          echo "Shell Script connect  Output: ${connect }"
        }

      }
    }

  }
}