pipeline{
  agent any{
    stages{
      stage("Checkout"){
        steps{
          echo "Checking out SCM"
          git url: "https://github.com/Mohan920228/learn-jenkins-app.git"
          branch: "main"
          credentialsId:"git hub login"
        }
      }
    }
  }
}