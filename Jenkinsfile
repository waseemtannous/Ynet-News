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
          withEnv(['JENKINS_RUNNER_VM= buntu@107.21.128.115']) {
            sh 'scp -o StrictHostKeyChecking=no build/libs/Ynet-News-0.0.1-SNAPSHOT.jar ${JENKINS_RUNNER_VM}:~/artifacts/Ynet-News-0.0.1-SNAPSHOT.jar'
            sh 'nohup ssh -o StrictHostKeyChecking=no ${JENKINS_RUNNER_VM} "java -jar ~/artifacts/Ynet-News-0.0.1-SNAPSHOT.jar > Ynet-News.out" &'
          }
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
