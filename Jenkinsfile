pipeline {
  agent any
  stages {
    stage('Application build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

  }
  environment {
    registry = 'thabie/cicd_pipeline'
  }
}