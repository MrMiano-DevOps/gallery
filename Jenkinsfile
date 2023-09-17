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

        stage ('Build') {
            steps {
                sh 'npm run'
            }
        }
    }
}