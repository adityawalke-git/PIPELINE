pipeline {
    agent any 

    parameters {
        string defaultValue: 'DEV', name: 'ENV'
    }

    triggers {
        pollSCM '* * * * *'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm			       
            }
        }
        stage('Build') {
            steps {
                sh '/home/aditya/Documents/apache-maven-3.9.6/bin/mvn install'
            }
        }
        stage('Deployment') {
            steps {
                script {
                    if (env.ENV == 'QA') {
                        sh 'cp target/PIPELINE.war /home/aditya/Documents/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been COMPLETED on QA!"
                    } else if (env.ENV == 'UAT') {
                        sh 'cp target/PIPELINE.war /home/aditya/Documents/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been done on UAT!"
                    }
                }
            }
        }
        stage('Slack') {
            steps {
                slackSend baseUrl: 'https://hooks.slack.com/services/', 
                          channel: 'april-fool', 
                          color: 'good', 
                          message: 'hello aditya', 
                          notifyCommitters: true, 
                          teamDomain: 'devops', 
                          tokenCredentialId: '203a64d0-f0f3-4953-96b4-3099bd20470e', 
                          username: 'slack'
            }
        }
    }
}
