pipeline {
  agent {
    node {
      label 'SlaveNode'
    }

  }
  stages {
    stage('test') {
      steps {
        sh 'aws eks list-clusters'
      }
    }

  }
}