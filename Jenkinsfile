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

        stage ('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage ('Deploy to Render') {
            steps {
                sh 'curl $RENDER_DEPLOY_HOOK'
            }
        }

    }

    post {
        failure {
            mail to: "${DEFAULT_RECIPIENTS}",
            subject: "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
            body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}"
        }
    }

    post {
        success {
            slackSend( channel: "anthony_ip1", token: env.SLACK_TOKEN_1, color: "good", message: "${custom_msg()}")
        }
    }

def custom_msg()
{
    def BUILD_ID = env.BUILD_ID
    def BUILD_STATUS = env.BUILD_STATUS

    def JENKINS_LOG = "BUILD # ${BUILD_ID} has ${BUILD_STATUS}"
}
}