pipeline {

  environment {
    registry = "https://registry.hub.docker.com"
    dockerImage = "jenkinsk8s"
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/srikanta1219/jenkins-k8s-deploy.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "kubeconfig")
        }
      }
    }

  }

}
