pipeline {
    agent any
    tools {
        maven 'Maven 3.8.1' // Replace with the name set in Global Tool Configuration
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "mvn clean install -Dmaven.test.skip=true"
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war'
            }
        }

        stage('Deployment') {
            steps {
                deploy adapters: [tomcat9(url: 'http://3.92.185.199:8080/', credentialsId: 'tomcat')], 
                       war: 'target/*.war', contextPath: 'app'
            }
        }

        stage('Notification') {
            steps {
                emailext(
                    subject: "Job Completed",
                    body: "Jenkins pipeline job for Maven build completed",
                    to: "sudheer.baraker@gmail.com"
                )
            }
        }
    }
}

