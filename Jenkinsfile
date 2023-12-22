pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Application Build') {
      steps {
        script {
          sh 'scripts/build.sh'
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('Test') {
      steps {
        script {
          sh 'scripts/test.sh'
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('Docker Image Build') {
      steps {
        script {
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('Docker Image Push') {
  steps {
    script {
      docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_id') {
        customImage.push("${env.BUILD_NUMBER}")
        customImage.push("latest")
      }
    }
  }
}

  }
  environment {
    registry = 'thabie/cicd_pipeline'
  }
  post {
    always {
      echo 'Pipeline completed.'
    }

    success {
      echo 'Pipeline succeeded!'
    }

    failure {
      echo 'Pipeline failed!'
    }

  }
}
