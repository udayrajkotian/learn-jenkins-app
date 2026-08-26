pipeline {
    agent any

    stages {
        stage('w/docker') {
            agent {
                docker{
                    image 'node:18-alpine'
                }
            }
                steps {
                    sh '''
                    npm --version
                    '''
            }
        }
   }
}