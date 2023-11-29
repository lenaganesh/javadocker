pipeline {
agent {
        docker {
          /*
           * Reuse the workspace on the agent defined at top-level of
           * Pipeline, but run inside a container.
           */
          reuseNode true
          image 'image: maven:3.6.3-openjdk-11'
        }
}
  environment {
    change_branch = ""
    change_target = ""
  }
  stages {
    stage('Trigger-Pull-Request-Build') {
      parallel {

          stage('EL6') {
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
              sh "ls -l ../"
              sh "hostname"

              build "javadocker-build"

            }
          }
        
      }
    }
  }
}