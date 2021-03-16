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
        slackSend channel: '#pipeline', message: 'Pipeline Notification', tokenCredentialId: 'slack_id'
      }
    }

  }
}
