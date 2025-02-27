pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    
                    pwd
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la

    
                '''
             }
         }
        stage('Test'){
            steps{
                echo 'test -f build/index.html'
            }
        }
    }
}
