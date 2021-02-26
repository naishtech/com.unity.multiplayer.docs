properties([pipelineTriggers([githubPush()])])
import java.text.SimpleDateFormat

def service_name ="test"

pipeline {
   agent {
      label "iit-jenkins-slave"
   }

    stages {
      stage('Sync with bucket') {
         steps {
            script{
               sync_bucket("mp-docs-unity-it-fileshare-test", "sa-mp-docs-test")
            }
         }
      }
      stage('Install nodejs and yarn') {
         steps {
            sh 'curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -'
            sh 'echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list'
            sh 'curl -fsSL https://deb.nodesource.com/setup_14.x | bash -'
            sh 'apt-get update && apt-get install -y nodejs yarn'
         }
      }
      stage('prepare env and install docusaurus') {
         steps {
            sh 'rm -rf temp'
            sh 'npx @docusaurus/init@latest init temp classic'
            sh 'yarn install'
         }
      }
      stage('Fix case issue on linux') {
         steps {
            sh 'cp -a static/img/transport/Pipeline-stages-diagram.png static/img/transport/pipeline-stages-diagram.png'
         }
      }
      stage('Build documentation') {
         steps {
            sh 'yarn build'
         }
      }
   }
}

def sync_bucket(BUCKET, CREDS) {
    withCredentials([file(credentialsId: CREDS, variable: 'SERVICEACCOUNT')]) {
      sh label: '', script: """
      gcloud auth activate-service-account --key-file ${SERVICEACCOUNT}
      gcloud auth configure-docker --quiet
      gsutil ls gs://mp-docs-unity-it-fileshare-test/
      """
     }
}