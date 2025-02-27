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

                    # Test step inside Build
                    test -f build/index.html
                    npm test
                '''
            }
        }
        stage('E2E'){

            agent{
                 docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jimmy'
                    reuseNode true
                    args '-u root:root'
                 }

            }
            step{
                sh '''

                 npm install -g serve
                 serve -s build 
                 npx playwright test
                 '''
            }
        }
          
    }
}
