pipeline {
    agent any
     label 'buildserver'
    }
    

    stages {
        stage('Build') {
            steps {
                sh "${MAVEN_HOME}/opt/apache-maven-3.9.6/bin/mvn clean package" // Build the application
            }
        }
        stage('Test') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn test" // Run tests
                  stash (name: 'Jenkins-CI-CD-Project', includes: "target/*.war")
            }
        }
        stage('Deploy') {
            agent {
                label 'tomcat1'
            steps {
                sh "${MAVEN_HOME}/bin/mvn deploy" // Deploy the application
                sh "~/apache-tomcat-7.0.94/bin/startup.sh"
        sh "sudo rm -rf ~/apache*/webapps/*.war"
        sh "sudo mv target/*.war ~/apache*/webapps/"
        sh "sudo systemctl daemon-reload"
        sh "~/apache-tomcat-7.0.94/bin/startup.sh &" // Using nohup to run Tomcat in the background
            }
        }
    }

    post {
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
