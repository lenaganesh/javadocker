def envAsString = '' // set as global variable
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
            script {
              envAsString = getEnvAsSring()
              echo "Env As String"
              echo "The Env sum is ${envAsString}"
            }
            build job: "javadocker-build", wait: true, parameters: [
              [$class: 'StringParameterValue', name: 'APS_COMPONENT_TITLE_TO_BUILD', value: "APS Home BE"}],
               [$class: 'StringParameterValue', name: 'PARENT_ENV', value: "${envAsString}"}],
            ]

          }
        }

      }
    }
  }
}
def getEnvAsSring() {
  def envAsStringTemp = ''
  sh 'env > env.txt'
  def list = readFile('env.txt').readLines()
  list.each {
    envAsStringTemp = envAsStringTemp + it + '\r\n'
  }
  return envAsStringTemp
  /*
  readFile('env.txt').split("\r?\n").each {
    echo it
    envAsStringTemp = envAsStringTemp + it + "\r\n"
  }
  return envAsStringTemp //envAsString
  */
}