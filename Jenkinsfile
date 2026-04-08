pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'ed1b780d-43eb-4d9c-838c-2911f70d013c'
        NETLIFY_AUTH_TOKEN = credentials('myNetlifyToken')
    }

    stages {
        /*
        stage('Docker'){
            steps{
                sh 'docker build -t my-docker-image .'
            }
        }
        */
        stage('Build'){
            agent{
                docker{
                    image "node:24.14-slim"
                    reuseNode true
                }
            }

            steps{
                sh'''
                    ls -la
                    node -v
                    npm -v
                    npm install
                    npm run build
                    ls -la
                '''
            }
        }
        
        stage('Test'){
            agent{
                docker{
                    image "node:24.14-slim"
                    reuseNode true
                }
            }
            
            steps{
                sh'''
                    test -f build/index.html
                    npm test
                '''
            }
        }      
    }
}