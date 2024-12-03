pipeline {
    agent any

    tools {
        jdk '11' // Specify the configured JDK in Jenkins
    }

    environment {
        GRADLE_OPTS = "-Dorg.gradle.daemon=false" // Disable Gradle daemon for consistent builds
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

 pipeline {
    agent any

    tools {
        jdk '11' // Ensure JDK 11 is installed in Jenkins
    }

    environment {
        JAVA_HOME = '/path/to/java11' // Replace with the actual Java 11 path
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
            deleteDir() // Alternative to cleanWs
        }
        success {
            echo 'Build pipeline completed successfully!'
        }
        failure {
            echo 'Build pipeline failed. Check the logs for details.'
        }
    }
}

        success {
            echo 'Build pipeline completed successfully!'
        }
        failure {
            echo 'Build pipeline failed. Check the logs for details.'
        }
    }
}
