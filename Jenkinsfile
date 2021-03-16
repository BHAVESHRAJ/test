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
        slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color: '#417a2a', message: "\n *GDPR Pipeline Deployment*: \n",)

   // post {
        // Send the build result to slack channel
     //   success {
       //   slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color:'good', message: "<@$userIds>Successfully deployed")
      //  }
       // failure {
           // slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color:'danger', message: "<@$userIds>Error in build ${env.JOB_NAME}")
       // }
   // }

      post {
        always {
            script {
                env.GIT_COMMIT_MSG = sh (script: 'git log -1 --pretty=%B ${GIT_COMMIT}', returnStdout: true).trim()
                env.GIT_AUTHOR = sh (script: 'git log -1 --pretty=%ae ${GIT_COMMIT} | awk -F "@" \'{print $1}\'', returnStdout: true).trim()
                slackSend(
                    color: color_slack_msg(),
                    message: "*${currentBuild.currentResult}:* Job `${env.JOB_NAME}` build `${env.BUILD_DISPLAY_NAME}` by <@${env.GIT_AUTHOR}>\n Build commit: ${GIT_COMMIT}\n Last commit message: '${env.GIT_COMMIT_MSG}'\n More info at: ${env.BUILD_URL}\n Time: ${currentBuild.durationString.minus(' and counting')}",
                    channel: 'pipeline-test',
                    tokenCredentialId: 'slack_id'
                )
            }
        }
    }

      }
    }

  }
}
