pipeline {
  agent none
  options {
      buildDiscarder(logRotator(numToKeepStr: '5')) 
      skipDefaultCheckout()
  }
  stages {
        stage('checkout') {
            agent any
            steps {
                checkout scm
            }
        }
        stage('build') {
          agent {
                docker {
                  args '-v /root/.m2:/root/.m2 -v /var/run/docker.sock:/var/run/docker.sock'
                  image 'maven:3-alpine'
                }
          }
          steps {
            script {
                def artifactId = sh(
                    returnStdout: true,
                    script: 'mvn help:evaluate -Dexpression=project.artifactId -q -DforceStdout'
                )
                def groupId = sh(
                    returnStdout: true,
                    script: 'mvn help:evaluate -Dexpression=project.groupId -q -DforceStdout'
                )
                echo "groupId is ${groupId}, artifactId is ${artifactId}"
                def artifactInfo = "groupId=${groupId} arifactId=${artifactId}"
                sh 'echo ${artifactInfo} > ./hello.txt'
                sh 'ls ./'
            }
          }
        }
  }
}
