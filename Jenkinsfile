pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        git(url: '/home/jenkins/gitrepos/javarepo.git', branch: 'master', poll: true)
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true install'
      }
      post {
        success {
          junit 'target/surefire-reports/**/*.xml'
          
        }
        
      }
    }
    stage('Build javarepo') {
      steps {
        build 'javarepo_1.0.x_ci'
      }
    }
    stage('Code Review') {
      steps {
        sleep 11
      }
    }
    stage('Test') {
      parallel {
        stage('Component Test') {
          steps {
            echo 'Component Test'
          }
        }
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
      }
    }
    stage('Deploy') {
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