pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage ('Test'){
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f 'build/index.html'
                    CI=true npm test -- --watchAll=false
                '''
            }
        }
        stage ('E2E'){
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.64.1-noble'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install --no-save serve
                    npx playwright test
                '''
            }
        }
    }
    post{
        always {
            junit testResults: 'test-results/*.xml', allowEmptyResults: true
        }
    }
}