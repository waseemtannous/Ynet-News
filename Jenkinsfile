pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'gradle clean build'
      }

      post {
      failure {
        script {
          slackSend(
            color: "#FF0000",
            channel: "personal-projects",
            message: "Ynet-News Build Status: FAILED"
          )
        }
      }

     success {
        script {
          slackSend(
            color: "#00FF00",
            channel: "personal-projects",
            message: "Ynet-News Build Status: SUCCESS"
          )
        }
      }
    }
    }

    



    stage('run') {
      steps {
        sh 'gradle run &'
      }

      failure {
        script {
          slackSend(
            color: "#FF0000",
            channel: "personal-projects",
            message: "Ynet-News Running Status: NOT RUNNING"
          )
        }
      }

     success {
        script {
          slackSend(
            color: "#00FF00",
            channel: "personal-projects",
            message: "Ynet-News Running Status: RUNNING"
          )
        }
      }
    }

    
  }
}
