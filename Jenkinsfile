pipeline {
    agent any
    tools {
        jdk '11'  // Use the available Java version on Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Setup Environment') {
            steps {
                sh './gradlew dependencies'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew assembleDebug'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/build/outputs/**/*.apk', fingerprint: true
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
