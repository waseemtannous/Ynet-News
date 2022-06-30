pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'chmod 400 gradlew'
        sh './gradlew clean build'
      }

      
    }

    stage('run') {
      steps {
        sh 'gradle run &'
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
