pipeline {
    agent any

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
                '''
            }
        }
    }
}