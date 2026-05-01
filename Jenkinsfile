pipeline {
    agent {
      label 'AGENT-1'
    }
    options {
        timeout(time: 300, unit: 'SECONDS')
        disableConcurrentBuilds()
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Name')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Info')
        booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Deploy app?')
        choice(name: 'ENV', choices: ['dev', 'qa', 'prod'], description: 'Environment')
        password(name: 'PASSWORD', defaultValue: '', description: 'Secret')
    }
    stages {
        stage('Use Parameters') {
            steps {
                echo "Hello ${params.PERSON}"
                echo "Environment: ${params.ENV}"

                script {
                    if (params.DEPLOY) {
                        echo "Deployment enabled"
                    } else {
                        echo "Deployment skipped"
                    }
                }

                echo "Bio: ${params.BIOGRAPHY}"

                // NEVER print password
                echo "Password received securely"
            }
        }
        stage('Approval') {
          input {
              message "Should we continue?"
              ok "Yes, we should."
              submitter "alice,bob"
              parameters {
                  string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
              }
          }
          steps {
              echo "Hello, ${PERSON}, nice to meet you."
          }
        }
        stage('Build') {
          steps {
            script {
              sh 'echo this is build'
            }
          }
        }
        stage('Test') {
          steps {
            script {
              sh 'echo this is test'
            }
          }
        }
        stage('Deploy') {
          when {
                expression { env.GIT_BRANCH?.contains('main') }
          }
          steps {
            script {
              sh 'echo this is deploy'
            }
          }
        }
    }

    post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
        success {
            echo "Build Successful"
        }
        failure {
            echo "Build Failed"
        }
        unstable {
            echo "Build Unstable"
        }
        changed {
            echo "Status changed from previous build"
        }
    }
}
