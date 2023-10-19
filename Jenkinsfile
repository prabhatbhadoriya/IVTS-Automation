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
          def scriptOutput = sh 'aws eks list-clusters --output json'
          echo "Shell Script Output: ${scriptOutput}"

          def connectWithRegion = sh 'aws eks update-kubeconfig --name monitoring-poc --region ap-south-1'
          echo "Shell Script connect  Output: ${connect }"

          def test3  = sh "aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,InstanceType,State.Name,PrivateIpAddress,PublicIpAddress]' --output table"
          def nodegroup_details = sh 'aws eks describe-nodegroup --cluster-name monitoring-poc --nodegroup-name primary'
        }

      }
    }

  }
}