pipeline{
  agent any
  environment{
    NETLIFY_SITE_ID= "5215a283-e542-4d4e-b83c-d648a46c1519"
    NETLIFY_AUTH_TOKEN=credentials('netlify-token')
  }
  stages{
    stage("Build"){
      agent{
        docker{
          image "node:trixie"
          reuseNode true
        }
      }
      steps{
        echo "in the docker container"
        sh '''
        ls -la
        node --version
        npm --version
        npm ci
        npm run build
        '''
      }
    }
    stage('Test') {
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
    stage("deploy"){
      agent {
                docker {
                    image "node:trixie"
                    reuseNode true
                }
            }
            steps{
            sh '''
            npm install netlify-cli
            node_modules/.bin/netlify --version
            node_modules/.bin/netlify status
        '''
    }
    } 
  }
}