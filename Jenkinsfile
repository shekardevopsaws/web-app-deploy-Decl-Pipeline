pipeline {

    agent any

    tools {
        maven 'maven 3.9.8'
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
                "http://54.147.63.142:8080/manager/html?path=/maven-web-application&update=true"
            """
            }

           
        }
    }
}
