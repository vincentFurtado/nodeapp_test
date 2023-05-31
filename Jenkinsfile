pipeline {

  environment {
    dockerimagename = "vincentfurtado/nodeapp"
    dockerImage = ""
  }

agent any 
  
  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/vincentfurtado/nodeapp_test.git'
      }
    }

    stage ('Container Image Builds') {
      sh 'sudo docker build -t vincentfurtado/nodeapp:latest .'
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
