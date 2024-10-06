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
        stage('Deploy'){
            agent{
                docker{
                    image 'node:19-apline'
                }
            }
            steps{
                sh '''
                    npm install netlify-cli -g
                    netlify --version
                '''
            }
        }

        /*stage('E2E'){
            agent{
                    docker{
                    image 'mcr.microsoft.com/playwright:v1.47.2-noble'
                    }
                }


            steps{
                sh'''
                    npm install serve 
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                '''
            }
         }*/

    
    }


   /* post {
        always {
                junit 'test-results/junit.xml'
        }
    }*/
}
