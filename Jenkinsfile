pipeline {
    agent any
    stages {
        stage("Build Notification"){
            slackSend channel: '#pipeline', message: 'Pipeline Notification', tokenCredentialId: 'slack_id'
        }
        stage("build") {
            steps {
                echo 'building the application'
            }
        }

        stage("test") {
            steps {
                echo 'testing the application'
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application'
            }
        }

    }
    
}
