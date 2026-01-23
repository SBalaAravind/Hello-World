pipeline {
    agent any

    tools {
        maven 'maven'
    }

    environment {
        TOMCAT_HOME = "/home/ubuntu/apache-tomcat-9.0.113"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SBalaAravind/Hello-World.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  cp webapp/target/webapp-1.0-SNAPSHOT.war $TOMCAT_HOME/webapps/
                '''
            }
        }
    }
}
