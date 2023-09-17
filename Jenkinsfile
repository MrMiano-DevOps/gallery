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

        stage ('Start server') {
            steps {
                sh 'node serve'
            }
        }
    }
}