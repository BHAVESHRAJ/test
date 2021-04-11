pipeline {
  agent any
  environment{
    BASE_JENKINS_URL = 'http://localhost:8080/job/Pipeline-slack/'
    BASE_REPO_URL = 'https://github.com/BHAVESHRAJ/test/commit'
  }  
  stages {
    stage('jenkins-start-notification'){
            steps{
                script{

                    if( env.GIT_COMMIT != null ){
                        env.TRUNCATED_GIT_COMMIT = env.GIT_COMMIT.take(10)
                    }else{
                        env.TRUNCATED_GIT_COMMIT = 'not defined'
                    }

                    if( env.GIT_PREVIOUS_SUCCESSFUL_COMMIT != null ){
                        env.TRUNCATED_LAST_SUCCESS_COMMIT = env.GIT_PREVIOUS_SUCCESSFUL_COMMIT.take(10)
                    }else{
                        env.TRUNCATED_LAST_SUCCESS_COMMIT = 'not defined'
                    }
                }

                slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color: '#1676c9', message: "\n *April Pipeline Deployment*: \n A deployment started on the *${GIT_BRANCH}* branch  \n\n *Build Number*: \t\t\t\t\t\t *Last Commit*\n ${BUILD_NUMBER}                   \t\t\t\t\t\t <${BASE_REPO_URL}/${GIT_COMMIT}|${TRUNCATED_GIT_COMMIT}> \n *Last Successful Commit* \n <${BASE_REPO_URL}/${GIT_PREVIOUS_SUCCESSFUL_COMMIT}|${TRUNCATED_LAST_SUCCESS_COMMIT}> \n\n To see the status of the deployment please <${BASE_JENKINS_URL}/${GIT_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n ")
            }
        }
    
    //stage ('Jenkins Start Notification') {
      //steps {
        // send build started notifications
        //slackSend (color: '#1676c9', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})", channel: 'pipeline-test', tokenCredentialId: 'slack_id')
      //}
    //}    
    stage("Build") {
      steps {
        echo "building..."
      }
    }
    stage("Test") {
      steps {
        echo "testing.."
      }
    }
    stage("Package") {
      steps {
        echo "packaging.."
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
            slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color: '#417a2a', message: "\n *April Pipeline Deployment*: \n The deployment No. *${BUILD_NUMBER}* was successful based on the changes on the *${GIT_BRANCH}* branch \n\n To see the deployment results please <${BASE_JENKINS_URL}/${GIT_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n ")
        }

        failure{
            echo 'Something went wrong'
            slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color: '#a8120a', message: "\n *April Pipeline Deployment*: \n The deployment *No.${BUILD_NUMBER}* has errors, please review the *${GIT_BRANCH}* branch \n\n To see the deployment errors please <${BASE_JENKINS_URL}/${GIT_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n ")
        }
    }
 
}
