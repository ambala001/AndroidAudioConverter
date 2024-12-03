pipeline {
    agent any
    tools {
        gradle 'Gradle 8.10'  // Updated to use Gradle 8.10
        jdk '11'             // Updated to use Java 11
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
