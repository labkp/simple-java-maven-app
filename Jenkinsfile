pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2 --network=host'
    }

  }
  stages {
    stage('Pararara') {
      parallel {
        stage('Paralel') {
          steps {
            echo 'parallel'
          }
        }
        stage('Build') {
          agent any
          steps {
            sh 'mvn -B -DskipTests clean package'
            echo 'Message'
          }
        }
        stage('error') {
          steps {
            echo 'Another'
          }
        }
      }
    }
    stage('Test') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'

        }

      }
      steps {
        sh 'mvn test'
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
      }
    }
    stage('Bye') {
      steps {
        echo 'Bye'
      }
    }
  }
}