pipeline {

  environment {
    dockerimagename = "ashish8290/hello-world-node "
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main', credentialsId: 'your-git-credentials', url:'https://github.com/Ashish-pand/Complete-CiCD-with-node-app.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhublogin'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
