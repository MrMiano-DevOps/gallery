pipeline {
    agent any
    tools { nodejs "Node"}
    stages {
        stage ('Clone repository') {
            steps {
                git 'https://github.com/MrMiano-DevOps/gallery.git'
            }
        }

        stage ('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage ('Deploy to Render') {
            steps {
                sh 'curl $RENDER_DEPLOY_HOOK'
            }
        }

        stage ('Test') {
            steps {
                sh 'npm te'
            }
        }

    post ('Failure Email Notification') {
            failure {
                mail bcc: '', body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

                Check console output at $BUILD_URL to view the results.''', cc: '', from: '', replyTo: '', subject: 'Jenkins Pipeline Failure', to: '$DEFAULT_RECIPIENTS'
            }
        }
    }
}