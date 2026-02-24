pipeline {
    agent any

    triggers {
        cron('H/5 * * * *')   // every 5 minutes (for timer builds)
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
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
                archiveArtifacts artifacts: 'target/**/*.*', fingerprint: true, allowEmptyArchive: true
            }
        }
    }
}
