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
