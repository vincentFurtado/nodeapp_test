pipeline {

  environment {
    dockerimagename = "vincentfurtado/nodeapp"
    dockerImage = ""
    env.PATH = "${dockerHome}/bin:${mavenHome}/bin:${env.PATH}"
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/vincentfurtado/nodeapp_test.git'
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
               registryCredential = 'dockerhub'
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
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubeconfig")
        }
      }
    }

  }

}
