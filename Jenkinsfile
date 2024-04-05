pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Your build steps (e.g., compile, package)
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                // Your test steps
                sh 'mvn test'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                // Your deployment steps
                // Example: deploying a WAR file to Tomcat
                sh 'cp target/*.war /path/to/tomcat/webapps'
            }
        }
    }
}
