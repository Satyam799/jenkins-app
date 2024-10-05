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
    }
   /* post {
        always {
                junit 'test-results/junit.xml'
        }
    }*/
}
