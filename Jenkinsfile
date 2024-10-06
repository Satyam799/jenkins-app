pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:19-alpine'
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm install --package-lock-only
                    npm ci
                    npm run build
                    ls -la
                    ls -la
                    '''
            }
        }
        stage('test'){
            agent{
                docker{
                    image 'node:19-alpine'
                }
            }


            steps{
                 echo 'Test stage'
                sh '''
                  #test -f build/index.html
                  npm test

                '''
                 echo 'a'
            }
        } 
        stage('E2E'){
            agent{
                    docker{
                    image 'node:mcr.microsoft.com/playwright:v1.47.2-noble'
                    }
                }


            steps{
                sh'''
                    npm run build
                    npm install -g serve 
                    serve -s build
                    npx playwrite test
                '''
            }
         }
    
    }


   /* post {
        always {
                junit 'test-results/junit.xml'
        }
    }*/
}
