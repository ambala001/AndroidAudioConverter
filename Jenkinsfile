pipeline {
    agent any

    tools {
        jdk '11' // Ensure JDK 11 is configured in Jenkins
    }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64' // Adjusted for your system's Java installation
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the source code...'
                checkout scm
            }
        }

        stage('Setup Environment') {
            steps {
                echo 'Setting up project dependencies...'
                sh './gradlew dependencies'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh './gradlew clean assembleDebug'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './gradlew test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archiving build outputs...'
                archiveArtifacts artifacts: '**/build/outputs/**/*.apk', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir() // Removes workspace files to free space
        }
        success {
            echo 'Build pipeline completed successfully!'
        }
        failure {
            echo 'Build pipeline failed. Check the logs for details.'
        }
    }
}
