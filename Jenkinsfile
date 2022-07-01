pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'chmod +x gradlew'
        sh './gradlew build'
      }
    }

     stage('Deploy') {
      steps {
        sshagent(['jenkinsRunner']) {
          sh 'scp -o StrictHostKeyChecking=no build/libs/Ynet-News-0.0.1-SNAPSHOT.jar ubuntu@3.84.212.195:~/artifacts/Ynet-News-0.0.1-SNAPSHOT.jar'
          sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.84.212.195 "(echo y\n | nohup java -jar Ynet-News-0.0.1-SNAPSHOT.jar) &"'
          // sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.84.212.195 " nohup java -jar Ynet-News-0.0.1-SNAPSHOT.jar & <<< y"'
        }
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
