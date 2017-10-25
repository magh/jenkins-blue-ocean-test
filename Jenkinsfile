pipeline {
    agent any
    tools { 
        maven 'maven 3.3.9' 
        jdk 'openjdk-8' 
    }

    stages {
        stage ('Initialize') {
            steps {
                git url: '/home/jenkins/gitrepos/javarepo.git', branch: 'master'
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
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
