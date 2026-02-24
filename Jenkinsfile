pipeline {
  agent any

  triggers {
    cron('H/5 * * * 1')  // every 5 minutes on Mondays
  }

  options {
    timestamps()
    disableConcurrentBuilds()
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build + Test') {
      steps {
        bat 'mvnw.cmd -B clean test'
      }
    }

    stage('JaCoCo Report') {
      steps {
        bat 'mvnw.cmd -B jacoco:report'
      }
    }

    stage('Archive Artifact') {
      steps {
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true, allowEmptyArchive: true
      }
    }
  }
}
