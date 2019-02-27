pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    DEPLOY_NAMESPACE = "jx-production"
  }
  stages {
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
          dir('env') {
            sh 'helm init --client-only --stable-repo-url http://charts.iflyresearch.com/ && helm repo add release http://chartmuseum.jx.yss && helm dependency build . && helm upgrade $DEPLOY_NAMESPACE . --install --namespace $DEPLOY_NAMESPACE'
          }
        }
      }
    }
  }
}
