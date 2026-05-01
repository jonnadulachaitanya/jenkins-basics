pipeline {
    agent {
      label 'AGENT-1'
    }
    options {
        timeout(time: 300, unit: 'SECONDS')
        disableConcurrentBuilds()
    }

    stages {
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
