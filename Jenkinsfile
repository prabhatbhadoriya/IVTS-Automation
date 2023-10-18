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
          def test3  = sh "aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,InstanceType,State.Name,PrivateIpAddress,PublicIpAddress]' --output table"
          def nodegroup_details = sh 'aws eks describe-nodegroup --cluster-name monitoring-poc --nodegroup-name primary'
          // Set your cluster and node group names
          def clusterName = 'monitoring-poc'
          def nodeGroupName = 'primary'

          // Get node group details
          def nodegroupDetails = sh(script: "aws eks describe-nodegroup --cluster-name ${clusterName} --nodegroup-name ${nodeGroupName}", returnStdout: true).trim()

          // Extract instance IDs from node group details
          def instanceIds = sh(script: "echo '${nodegroupDetails}' | jq -r '.nodegroup.resources[].ec2Instances[].id'", returnStdout: true).trim()

          // Display instance details
          sh "aws ec2 describe-instances --instance-ids ${instanceIds} --query 'Reservations[*].Instances[*].[InstanceId,InstanceType,State.Name,PrivateIpAddress,PublicIpAddress]' --output table"
        }

      }
    }

  }
}