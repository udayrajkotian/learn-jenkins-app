pipeline{
    agent any

    stages{
        stage{('Build') {
            agent {
                docker{
                    image 'node:18-alpine'
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

        }
        stage ('test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                -f ['build/index.html'] && echo "file exists" || echo "file does not exist"
                '''
            }
        }
    }
}