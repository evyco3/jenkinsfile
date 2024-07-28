pipeline {
    agent any

    tools {
        maven 'Maven' // Adjust as per your Maven installation name in Jenkins
        jdk 'JDK21'  // Adjust as per your JDK installation name in Jenkins
    }

    environment {
        GITHUB_CREDENTIALS = credentials('evy') // Replace with your Jenkins credential ID for GitHub
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/evyco3/jenkinsfile.git', credentialsId: "${GITHUB_CREDENTIALS}"
            }
        }
        stage('Build and Test') {
            steps {
                sh 'mvn clean test'
            }
        }
        stage('Generate Allure Report') {
            steps {
                sh 'mvn allure:report'
            }
        }
        stage('Publish Allure Report') {
            steps {
                allure includeProperties: false, jdk: '', results: [[path: 'target/allure-results']]
            }
        }
    }
}
