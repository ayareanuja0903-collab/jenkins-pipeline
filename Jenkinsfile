pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/ayareanuja0903-collab/jenkins-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop node-container || true
                docker rm node-container || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name node-container node-app'
            }
        }

        stage('Clean Images') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }
}