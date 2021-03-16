pipeline {
  agent any
  stages {
    stage("Build") {
      steps {
        echo "building..."
      }
    }
    stage("Test") {
      steps {
        echo "testing..."
      }
    }
    stage("Package") {
      steps {
        echo "packaging..."
      }
    }
    stage("Notification") {
      steps {
        //slackSend channel: '#pipeline', color: '#417a2a', message: 'Pipeline Notification', tokenCredentialId: 'slack_id'
        echo 'The pipeline finish successfully'
        slackSend (channel: '#pipeline', tokenCredentialId: 'slack_id' color: '#417a2a', message: "\n *Pipeline Deployment*: \n The deployment No. *${BUILD_NUMBER}* was successful based on the changes on the *${GIT_LOCAL_BRANCH}* branch \n\n To see the deployment results please <${BASE_JENKINS_URL}/${GIT_LOCAL_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n ")
      }
    }

  }
}
