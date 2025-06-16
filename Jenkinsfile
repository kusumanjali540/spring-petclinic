pipeline {
    agent any

    tools {
        maven 'Maven' 
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/kusumanjali540/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

          stage('Deploy to Tomcat') {
            steps {
                sh '''
                    curl -T target/spring-petclinic-*.jar \
                    "http://tomcat-user:tomcat-pass@localhost:8081/manager/text/deploy?path=/petclinic&update=true"
                '''
            }
        }
    }
}
