pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = 'b4e73f81-e3aa-4c26-8bf1-42b24bc323d8'
        NETLIFY_AUTH_TOKEN = credentials('tech2102-assign2-token')
    }

    stages {
        stage('Build'){
            agent{
                docker{
                    image 'node:22.14.0-alpine3.21'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test'){
            agent{
                docker{
                    image 'node:22.14.0-alpine3.21'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
        stage('Deploy'){
            agent{
                docker{
                    image 'node:22.14.0-alpine3.21'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploy to Site ID: $NETLIFY_SITE_ID"
                    node_modules/.bin/netlify deploy --prod --dir=build
                '''
            }
        }
    }
}