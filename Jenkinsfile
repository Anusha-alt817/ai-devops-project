pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        ACCOUNT_ID = '559401928438'
        REPOSITORY = 'ai-backend'
        IMAGE_TAG = 'v1'
    }

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t ai-backend:v1 .'
            }
        }

        stage('AWS Login') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | \
                docker login --username AWS --password-stdin \
                $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
                '''
            }
        }

        stage('Tag Image') {
            steps {
                sh '''
                docker tag ai-backend:v1 \
                $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$REPOSITORY:v1
                '''
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                docker push \
                $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$REPOSITORY:v1
                '''
            }
        }
    }
}
