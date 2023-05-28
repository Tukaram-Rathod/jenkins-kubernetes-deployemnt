'''pipeline {

  environment {
    dockerimagename = "tukaramrathod02/react-app"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/Tukaram-Rathod/jenkins-kubernetes-deployemnt.git'
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
               registryCredential = 'DockerHub_Crediential'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}'''
pipeline {
  agent any
  }
  stages {
    stage('Build') {
      steps {
        // Checkout code from version control system
        git 'https://github.com/Tukaram-Rathod/jenkins-kubernetes-deployemnt.git'
        
        // Build Docker image
        sh 'docker build -t tukaramrathod02/react-app:v1 .'
        
        // Push Docker image to a registry
        sh 'docker push tukaramrathod02/react-app:v1'
      }
    }
    stage('Deploy') {
      steps {
        // Deploy to Kubernetes cluster
        sh 'kubectl apply -f deployemnts.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }
    stage('Test') {
      steps {
        // Deploy to Kubernetes cluster
        sh 'kubectl get pod'
        sh 'kubectl get node'
      }
    }
  }  
}
