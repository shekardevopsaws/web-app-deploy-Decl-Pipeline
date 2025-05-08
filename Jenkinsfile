pipeline {

    agent any

    tools {
        maven 'maven 3.9.8'
    }

    environment {
        SLACK_CHANNEL = '#new-channel'
        SLACK_CREDENTIAL_ID = 'slack-webhook'
        SLACK_WEBHOOK_URL = 'https://hooks.slack.com/services/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'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'dev', 
                    credentialsId: '65ee34e4-4229-4aad-bd3e-5c0eca7de468', 
                    url: 'https://github.com/shekardevopsaws/web-app-deploy-Decl-Pipeline.git'
            }
        }

        stage('Build the source code') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Scan Source code') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }

        
        stage('Deploy artifacts to Nexus') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('deploy app into Webpage')
        {

            steps{

                echo "Deploying WAR file using curl..."

            sh """
                curl -u mamatha:mamatha123 \
                --upload-file /var/lib/jenkins/workspace/war-Project/target/maven-web-application.war \
                "http://54.147.63.142:8080/manager/text/deploy?path=/maven-web-application&update=true"

            """
            }

           
        }//stage ended

        

    }//stages ended



// Notifications to slack




    post {
       success {
        sh """
        curl -X POST -H 'Content-type: application/json' \
        --data '{"text":"✅ *SUCCESS*: Job ${env.JOB_NAME} #${env.BUILD_NUMBER} completed successfully!"}' \
        ${SLACK_WEBHOOK_URL}
        """
      }
      failure {
        sh """
        curl -X POST -H 'Content-type: application/json' \
        --data '{"text":"❌ *FAILURE*: Job ${env.JOB_NAME} #${env.BUILD_NUMBER} failed!"}' \
        ${SLACK_WEBHOOK_URL}
        """
      }
    
    }
}




