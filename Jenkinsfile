pipeline {
  agent {
    docker {
      image '3.6.1-jdk-8-alpine '
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('duild') {
      parallel {
        stage('Build') {
          steps {
            sh 'mvn -B -DskipTests clean package'
          }
        }
        stage('cuild') {
          steps {
            echo 'building, please wait...'
          }
        }
      }
    }
  }
}