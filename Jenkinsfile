pipeline {
    agent any
    tools {
        maven 'Maven' // Use the name you specified in Jenkins Global Tool Configuration
    }
    environment {
        // Define your deployment credentials id
        // This should be pre-configured in Jenkins credentials store
        TOMCAT_CREDENTIALS_ID = 'tomcat-deployer-credentials'
    }

    stages {
        stage('Build') {
            steps {
                // Build your project with Maven
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // Run your tests
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy to Tomcat manually using Curl

                    sh "curl --upload-file ./target/*.war 'http://admin:admin@3.95.156.67:8081/manager/text/deploy?path=/WebAppCal&update=true'"

                }
            }
        }
    }
}

