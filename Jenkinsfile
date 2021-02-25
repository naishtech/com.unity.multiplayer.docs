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
            sh 'curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -'
            sh 'echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list'
	    sh 'curl -fsSL https://deb.nodesource.com/setup_14.x | bash -'
	    sh 'apt-get update && apt-get install -y nodejs yarn'
            sh 'rm -rf temp'
            sh 'npx @docusaurus/init@latest init temp classic'
            sh 'yarn install'
            /* sh 'npm update --force' */
            sh 'cp -a static/img/transport/Pipeline-stages-diagram.png static/img/transport/pipeline-stages-diagram.png'
            sh 'yarn build'
            sh 'ls -lah build'
         }
      }
   }
}
