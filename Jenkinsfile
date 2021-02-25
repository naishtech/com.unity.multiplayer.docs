properties([pipelineTriggers([githubPush()])])
import java.text.SimpleDateFormat

def service_name ="test"

pipeline {
   agent {
      label "iit-jenkins-slave"
   }
    stages {
      stage('build') {
         steps {
            sh 'uptime && date && ls -lah'
         }
      }
   }
}
