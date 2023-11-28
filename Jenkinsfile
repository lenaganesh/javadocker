pipeline {
  agent {
    label "docker-build-java-agent"
  }
  environment {
    change_branch = ""
    change_target = ""
  }
  stages {
    stage('Trigger-Pull-Request-Build') {
      steps {

        sh 'printenv'
        echo "Trigger devops main job to build"
        script {
          if (env.CHANGE_ID != null) {
            change_id = "${CHANGE_ID}"
          } else {
            change_id = ""
          }
          if (env.CHANGE_TARGET != null) {
            change_target = "${CHANGE_TARGET}"
          } else {
            change_target = ""
          }
        }
        sh "pwd"
        sh "ls -l"
        sh "hostname"
        sh "ip a"

        build job: "javadocker-build", wait: true
      }
    }
  }
}
