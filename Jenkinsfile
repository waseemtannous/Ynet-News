pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'chmod +x gradlew'
        sh './gradlew clean build'
      }

      
    }

    stage('run') {
      steps {
        sh './gradlew run &'
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
