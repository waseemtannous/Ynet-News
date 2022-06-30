pipeline {
  agent any
  stages {
    stage('build and run') {
      steps {
        sh 'chmod +x gradlew'
        sh './gradlew bootrun'
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
