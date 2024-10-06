pipeline {
    agent any
    
    environment{
        NETLIFY_SITE_ID='b29cf13d-6566-4cae-abec-4946331c44dc'
        NETLIFY_AUTH_TOKEN=credentials('netlify-token')
    }
    
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
                    image 'node:19-alpine'
                }
            }
            steps{
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploy to the production. SITE ID : $NETLIFY_SITE_ID"
                    node_modules/.bin/netlify status
                    node_modules/.bin/netlify deploy --dir=build --prod
                    
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
