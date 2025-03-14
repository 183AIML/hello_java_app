pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Apache Maven 3.9.9'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/183AIML/hello_java_app.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                bat "${MAVEN_HOME}/bin/mvn clean compile"
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat "${MAVEN_HOME}/bin/mvn test"
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the app...'
                bat "${MAVEN_HOME}/bin/mvn package"
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}