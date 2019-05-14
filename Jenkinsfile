pipeline {
    agent any

    tools {
        maven 'localMaven'
    }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean seedstack:release'
            }
            post {
                success {
                    echo 'Now Archiving...'
                }
            }
        }

        stage ('Tests'){
            steps {
                sh """
                     mkdir -p selenium-screenshots/error
                     /usr/bin/mvn -B -f selenium/pom.xml clean test -X
                   """
            }
        }

        stage ('Clean up'){
            steps {
                cleanWs()
            }
        }
    }
}