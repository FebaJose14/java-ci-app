pipeline {
    agent any

    tools {
        maven 'Maven-3'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                echo 'Compiling Java source code using Maven...'
                sh 'mvn clean compile'
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo 'Running JUnit tests...'
                sh 'mvn test'
            }
        }

        stage('Package Application') {
            steps {
                echo 'Packaging application into a JAR artifact...'
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully! Archiving artifacts...'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        failure {
            echo 'Pipeline failed during execution. Please check the logs.'
        }
    }
}
