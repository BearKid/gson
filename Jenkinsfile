pipeline {
  agent {
    docker {
      args '-v /root/.m2:/root/.m2'
      image 'maven:3.6.1-jdk-8'
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('print build') {
          steps {
            sh 'echo "hello world"'
          }
        }
        stage('build') {
          steps {
            sh 'mvn -B -DskipTests clean package'
          }
        }
        stage('error') {
          steps {
            echo 'build print message'
          }
        }
      }
    }
  }
}