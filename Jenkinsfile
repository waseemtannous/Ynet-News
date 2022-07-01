pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'chmod +x gradlew'
        sh './gradlew build'
      }
    }

     stage('Run') {
      steps {
        // sh 'ls -la build/libs/'
        // sh 'nohup java -jar build/libs/Ynet-News-0.0.1-SNAPSHOT.jar &'
        // sh 'nohup java -jar build/libs/Ynet-News-0.0.1-SNAPSHOT.jar >> /tmp/ynet.log 2>&1&'
        // sh 'nohup java -jar build/libs/Ynet-News-0.0.1-SNAPSHOT.jar >> server.log 2>&1&'
        sh 'echo "java -jar build/libs/Ynet-News-0.0.1-SNAPSHOT.jar" | at now + 1 minutes'
        // sh './gradlew bootrun &'
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
