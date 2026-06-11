pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t ai-backend:v1 .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f ai-backend || true
                docker run -d --name ai-backend -p 4001:4000 ai-backend:v1
                '''
            }
        }
    }
}
