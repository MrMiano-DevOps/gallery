pipeline {
    agent any
    tools { nodejs "Node"}
    environment {
        IP1_PROJECT_URL = "https://my-ip1-node-app.onrender.com/"
    }
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
                sh 'npm test'
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
}