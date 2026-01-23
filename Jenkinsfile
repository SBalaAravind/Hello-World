pipeline {
    agent any

    environment {
        // Optional: JAVA_HOME, MAVEN_HOME set chesuko
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/SBalaAravind/Hello-World.git'
            }
        }

        stage('Build') {
            steps {
                // Maven clean + package
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                // Copy WAR to Tomcat webapps folder
                sh '''
                cp webapp/target/webapp-1.0-SNAPSHOT.war \
                /home/ubuntu/apache-tomcat-9.0.113/webapps/webapp.war
                '''
            }
        }
    }

    post {
        success {
            echo "Build & Deploy SUCCESS ✅"
        }
        failure {
            echo "Build or Deploy FAILED ❌"
        }
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
