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
          current_time=$(date +"%H:%M")
          echo "Current time in 24-hour format: $current_time"

          // sh 'date +%H:%M'
          def scriptOutput = sh(script: 'aws eks list-clusters --output json', returnStdout: true).trim()
          def jsonSlurper = new groovy.json.JsonSlurper()
          def json = jsonSlurper.parseText(scriptOutput)





          echo "Shell Script Output: ${scriptOutput}"

          echo "json Script Output: ${json.clusters[0]}"

          def connectWithRegion = sh 'aws eks update-kubeconfig --name monitoring-poc --region ap-south-1'
          sh 'kubectl get nodes -l eks.amazonaws.com/nodegroup=primary'

          def test3  = sh "aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,InstanceType,State.Name,PrivateIpAddress,PublicIpAddress]' --output table"
          def nodegroup_details = sh 'aws eks describe-nodegroup --cluster-name monitoring-poc --nodegroup-name primary'
        }

      }
    }

  }
}