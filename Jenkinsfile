pipeline {
  agent any
  stages {
    stage ('Jenkins Start Notification') {
      steps {
        // send build started notifications
        slackSend (color: '#1676c9', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})", channel: 'pipeline-test', tokenCredentialId: 'slack_id')
      }
    }    
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
    //stage("Notification") {
    //  steps {
        //slackSend channel: '#pipeline', color: '#417a2a', message: 'Pipeline Notification', tokenCredentialId: 'slack_id'
    //   echo 'The pipeline finish successfully'
        //slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color: '#417a2a', message: "\n *GDPR Pipeline Deployment*: \n",)
        //  slackSend(color: '#417a2a', message: "*${currentBuild.currentResult}:* Job `${env.JOB_NAME}` build `${env.BUILD_DISPLAY_NAME}` by <@${env.GIT_AUTHOR}>\n Build commit: ${GIT_COMMIT}\n Last commit message: '${env.GIT_COMMIT_MSG}'\n More info at: ${env.BUILD_URL}\n Time: ${currentBuild.durationString.minus(' and counting')}", channel: 'pipeline-test', tokenCredentialId: 'slack_id')
    // }
   // }
  }
 post{

        success{
            echo 'The pipeline finish successfully'
            slackSend (color: '#417a2a', message: "*${currentBuild.currentResult}:* Job `${env.JOB_NAME}` build `${env.BUILD_DISPLAY_NAME}` by <@${env.GIT_AUTHOR}>\n Build commit: ${GIT_COMMIT}\n Last commit message: '${env.GIT_COMMIT_MSG}'\n More info at: ${env.BUILD_URL}\n Time: ${currentBuild.durationString.minus(' and counting')}", channel: 'pipeline-test', tokenCredentialId: 'slack_id')
        }

        failure{
            echo 'Something went wrong'
            slackSend (color: '#a8120a', message: "*${currentBuild.currentResult}:* Job `${env.JOB_NAME}` build `${env.BUILD_DISPLAY_NAME}` by <@${env.GIT_AUTHOR}>\n Build commit: ${GIT_COMMIT}\n Last commit message: '${env.GIT_COMMIT_MSG}'\n More info at: ${env.BUILD_URL}\n Time: ${currentBuild.durationString.minus(' and counting')}", channel: 'pipeline-test', tokenCredentialId: 'slack_id')
        }
    }
 
}
