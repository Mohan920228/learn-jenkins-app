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
                    ls -la
                    node --version
                    npm --version

                    npm ci
                    npm run build

                    find . -path "*/build/index.html"

                    CI=true npm test
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
        stage("Paralleltest"){
            parallel {
                stage("docker cont runner"){
                    agent{
                        docker{
                            image "httpd:trixie"
                        }
                }
                    steps{
                        sh "ls"
                }
            }
                stage("Paralleltest2"){
                    agent{
                        docker{
                          image "memcached:trixie"
                    }
                }
                    steps{
                        sh "ls"
                }
            }
        }
    }
    }
    
}