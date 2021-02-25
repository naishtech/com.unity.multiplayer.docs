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
            sh 'curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -'
            sh 'echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list'
            sh 'apt-get update && apt-get install -y --no-install-recommends nodejs yarn'
         }
      }
   }
}
