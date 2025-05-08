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

        // Uncomment this when you're ready to push to Nexus
        // stage('Deploy artifacts to Nexus') {
        //     steps {
        //         sh 'mvn deploy'
        //     }
        // }
    }
}
