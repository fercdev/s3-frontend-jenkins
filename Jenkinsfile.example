pipeline {
    agent {
            docker {
                image 'node:18-alpine'
            }
    }

    environment {
       VERCEL_TOKEN = credentials('vercel-token')
    }

    stages {
        stage('Build react app') {
            steps {
                sh '''
                    npm install -g vercel
                    vercel --prod --token=$VERCEL_TOKEN --confirm
                '''
            }
        }
    }
}