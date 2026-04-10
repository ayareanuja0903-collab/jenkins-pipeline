pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker ps -q --filter "name=node-container" | grep -q . && docker stop node-container || true
                docker ps -aq --filter "name=node-container" | grep -q . && docker rm node-container || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name node-container node-app'
            }
        }
    }
}