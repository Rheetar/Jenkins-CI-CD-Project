pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven' // Assumes that you have configured Maven tool in Jenkins
    }

    stages {
        stage('Build') {
            steps {
                sh "${env.MAVEN_HOME}/bin/mvn clean package" // Build the Maven project
            }
        }
        stage('Test') {
            steps {
                sh "${env.MAVEN_HOME}/bin/mvn test" // Run tests
            }
        }
        stage('Deploy') {
            steps {
                sh "${env.MAVEN_HOME}/bin/mvn deploy" // Deploy the WAR file
            }
        }
    }

    post {
        always {
            // Clean up actions (if any)
        }
        success {
            echo 'Pipeline executed successfully!' // Display success message
        }
        failure {
            echo 'Pipeline execution failed!' // Display failure message
        }
    }
}
