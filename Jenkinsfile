pipeline {
    agent any

    tools {
        jdk 'Java-17'
        maven 'Maven-3.9.6'
    }

    environment {
        TOMCAT_HOME = "/home/ubuntu/apache-tomcat-9.0.115"
        WAR_NAME = "webapp-1.0-SNAPSHOT.war"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/SBalaAravind/Hello-World.git'
            }
        }

        stage('Build WAR with Maven') {
            steps {
                sh '''
                mvn clean package -DskipTests
                '''
            }
        }

        stage('Stop Tomcat') {
            steps {
                sh '''
                if pgrep -f tomcat > /dev/null
                then
                  $TOMCAT_HOME/bin/shutdown.sh
                  sleep 10
                fi
                '''
            }
        }

        stage('Deploy WAR') {
            steps {
                sh '''
                rm -rf $TOMCAT_HOME/webapps/webapp-1.0-SNAPSHOT*
                cp webapp/target/$WAR_NAME $TOMCAT_HOME/webapps/
                '''
            }
        }

        stage('Start Tomcat') {
            steps {
                sh '''
                $TOMCAT_HOME/bin/startup.sh
                sleep 20
                '''
            }
        }

        stage('Verify App') {
            steps {
                sh '''
                curl -I http://localhost:8090/webapp-1.0-SNAPSHOT/ || true
                '''
            }
        }
    }

    post {
        success {
            echo "✅ CI/CD Pipeline SUCCESS – App Deployed"
        }
        failure {
            echo "❌ Pipeline FAILED – Check logs"
        }
    }
}

            }
        }
    }
}
