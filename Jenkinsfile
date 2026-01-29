pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'jdk17'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Check WAR') {
            steps {
                sh 'ls -l webapp/target'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@18.216.64.238 \
                "rm -rf /opt/tomcat/webapps/*"

                scp -o StrictHostKeyChecking=no \
                webapp/target/*.war \
                ubuntu@18.216.64.238:/opt/tomcat/webapps/
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}

