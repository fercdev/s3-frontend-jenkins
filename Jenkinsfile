pipeline {
    agent none

    environment {
        AWS_REGION = 'us-east-1'
        BUCKET_NAME = 'mi-bucket-codigo-cf'
    }

    stages {
        stage('Build react app') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }

            steps {
                sh "npm install"
                sh "npm run build"
                sh "cp build/index.html build/error.html"
            }
        }


        stage('Deploy s3') {
            agent {
                docker {
                    image 'amazon/aws-cli:latest'
                    args '--entrypoint ""'
                }
            }
            
            steps {
                withAWS(credentials: 'aws-credentials', region: "${AWS_REGION}") {
                    sh '''
                        aws s3 sync build/ s3://${BUCKET_NAME}/ --delete
                    '''
                }
            }
        }
    }
}