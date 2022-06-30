pipeline {
  agent any
  stages {
    stage('build and run') {
      steps {
        sh 'chmod +x gradlew'
        sh './gradlew jar'
        sh 'java -jar build/libs/Ynet-News-0.0.1-SNAPSHOT.jar &'
      }
    }
  }

  post {
      failure {
        script {
          slackSend(
            color: "#FF0000",
            channel: "personal-projects",
            message: "Ynet-News Status: FAILED"
          )
        }
      }

     success {
        script {
          slackSend(
            color: "#00FF00",
            channel: "personal-projects",
            message: "Ynet-News Status: SUCCESS"
          )
        }
      }
    }
}
