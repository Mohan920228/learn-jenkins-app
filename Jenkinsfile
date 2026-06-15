pipeline {
    agent any

    stages {

        stage("Build") {
            agent {
                docker {
                    image "node:trixie"
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
                '''
            }
        }

        stage("Test") {
            agent {
                docker {
                    image "node:trixie"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    CI=true npm test
                '''
            }
        }

        stage("Deploy") {
            agent {
                docker {
                    image "node:trixie"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli

                    ./node_modules/.bin/netlify --version
                '''
            }
        }
    }
}