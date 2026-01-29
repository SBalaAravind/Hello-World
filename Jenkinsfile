pipeline {
    agent any

    tools {
        maven 'maven'
    }

    environment {
        DEPLOY_USER = "ubuntu"
        DEPLOY_HOST = "18.216.64.238"
        TOMCAT_HOME = "/opt/tomcat"
        DEPLOY_PATH = "/opt/tomcat/webapps"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                git branch: 'master',
                    url: 'https://github.com/SBalaAravind/Hello-World.git'
            }
        }

        stage('Build WAR') {
            steps {
                echo 'Building WAR using Maven'
                sh 'mvn clean package'
            }
        }

        stage('Check WAR') {
            steps {
                sh 'ls -l target'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh """
                ssh ${DEPLOY_USER}@${DEPLOY_HOST} '
                    rm -rf ${DEPLOY_PATH}/Hello-World*
                '

                scp target/*.war \
                    ${DEPLOY_USER}@${DEPLOY_HOST}:${DEPLOY_PATH}/

                ssh ${DEPLOY_USER}@${DEPLOY_HOST} '
                    ${TOMCAT_HOME}/bin/shutdown.sh || true
                    sleep 5
                    ${TOMCAT_HOME}/bin/startup.sh
                '
                """
            }
        }
    }

    post {
        success {
            echo '✅ WAR deployed successfully to Tomcat'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}
