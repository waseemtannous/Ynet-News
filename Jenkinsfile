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
        sh 'scp -v -o StrictHostKeyChecking=no  -i /var/lib/jenkins/secrets/3.84.212.195 build/libs/Ynet-News-0.0.1-SNAPSHOT.jar root@3.84.212.195:/home/artifacts/Ynet-News-0.0.1-SNAPSHOT.jar'
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
