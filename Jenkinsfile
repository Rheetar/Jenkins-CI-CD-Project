pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        label 'node-buildserver'
      }
      steps {
        echo 'Building the application'
        //Define build steps here
        sh '/opt/maven/bin/mvn clean package'
      }
    }
    stage('Test') {
      agent {
        label 'node-buildsrever'
      }
    steps {
      echo 'Running tests'
      //Define test steps here
      sh 'mvn test'
      stash (name: 'Jenkins-ci-cd-Project', includes: "target/*war")
    }
    }
    stage('Deploy') {
      agent {
        label 'node-tomcat'
      }
      steps {
        echo 'Deploying the application'
        //Define deployment steps here
        unstash 'jenkins-ci-cd-Project'
        sh "sudo rm -rf ~/apache*/webapp/*.war"
        sh "sudo mv target/*.war ~/apache*/webapps/"
        sh "sudo systemctl daemon-reload"
        sh "sudo ~/apache-tomcat-7.0.94/bin/shutdown.sh && sudo ~/apache-tomcat-7.0.94/bin/startup.sh"
        }
        }
    }
 post {
        always {
            // Send email notification on completion
            emailext (
                body: "Check console output at $BUILD_URL to see results,",           
                subject: "Jenkins Build ${currentBuild.currentResult} jenkins-ci-cd-Project",
                to: "blessingritaa@gmail.com", 
                mimeType: 'text/html'
            )
        }
    }
}
   
