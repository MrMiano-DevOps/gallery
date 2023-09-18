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
    }

    post {
            failure {
                emailext body: 'Your pipeline has failed', subject: 'Jenkins Pipeline Failure', to: 'anthony.maina@student.moringaschool.com'
            }
    }
}
