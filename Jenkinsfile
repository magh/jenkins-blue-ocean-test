pipeline {
  agent any
  stages {
    stage('Deploy to staging') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true install'
      }
      post {
        success {
          junit 'target/surefire-reports/**/*.xml'
          
        }
        
      }
    }
    stage('Test') {
      parallel {
        stage('Upgrade Test') {
          steps {
            echo 'Upgrade Test'
          }
        }
        stage('Integration Test') {
          steps {
            echo 'Integration Test'
          }
        }
        stage('Manual Test') {
          steps {
            echo 'Manual Test'
            input 'Waiting for interactive input'
          }
        }
        stage('End to end Test') {
          steps {
            sleep 1
          }
        }
        stage('Security scanning') {
          steps {
            sleep 1
          }
        }
      }
    }
    stage('Deploy to release') {
      steps {
        echo 'Deploying....'
      }
    }
  }
  tools {
    maven 'maven 3.3.9'
    jdk 'openjdk-8'
  }
}