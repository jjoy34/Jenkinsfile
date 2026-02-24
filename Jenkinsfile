pipeline {
  agent any

  triggers {
    cron('H/5 * * * 1')
  }

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build + Test') {
      steps {
        bat 'mvn -B clean test'
      }
    }

    stage('JaCoCo Report') {
      steps {
        bat 'mvn -B jacoco:report'
      }
      post {
        always {
          jacoco(
            execPattern: '**/target/*.exec, **/target/jacoco.exec',
            classPattern: '**/target/classes',
            sourcePattern: '**/src/main/java'
          )
        }
      }
    }

    stage('Archive Artifact') {
      steps {
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
      }
    }

  }
}
