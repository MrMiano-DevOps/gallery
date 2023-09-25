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
    

        success {
            slackSend( channel: "#anthony_ip1", color: "good", message: "Pipeline Name: ${env.JOB_NAME} \n\nBuild Number: ${env.BUILD_ID} \n\n Build Status: ${currentBuild.currentResult} \n\nBuild duration: ${currentBuild.duration}\n\nThe application can be accessed here: ${IP1_PROJECT_URL}")
        }
    }
}