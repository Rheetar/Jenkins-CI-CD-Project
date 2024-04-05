pipeline {
    agent {
        label 'buildserver'
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application'
                // Define build steps here
                sh '/opt/maven/bin/mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests'
                // Define test steps here
                sh 'mvn test'
                stash (name: 'Jenkins-CI-CD-Project', includes: "target/*.war")
            }
        }
        stage('Deploy') {
            agent {
                label 'tomcat1'
            }
            steps {
                echo 'Deploying the application'
                // Define deployment steps here
                unstash 'Jenkins-CI-CD-Project'
                sh "sudo rm -rf ~/apache*/webapps/*.war"
                sh "sudo mv target/*.war ~/apache*/webapps/"
                sh "sudo systemctl daemon-reload"
                sh "sudo ~/apache*/bin/shutdown.sh && sudo ~/apache*/bin/startup.sh"
            }
        }
    }
    post {
        success {
            mail to: "blessingritaa@gmail.com",
            subject: "Jenkins-CI-CD-Project Successful",
            body: "Jenkins-CI-CD-Project was successfully built, tested, and deployed"
        }
        failure {
            mail to: "blessingritaa@gmail.com",
            subject: "Jenkins-CI-CD-Project Failed",
            body: "Jenkins-CI-CD-Project failed, please investigate"
        }
    }
}
