pipeline {
    agent any

    tools {
        maven 'Maven' // Adjust as per your Maven version
        jdk 'JDK21' // Adjust as per your JDK version
        git 'Git'
    }

    environment {
        GITHUB_CREDENTIALS = credentials('evy') // Replace with your Jenkins credential ID for GitHub
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/evyco3/jenkinsfile.git', branch: 'evy', credentialsId: 'evy'
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
                allure includeProperties: false, results: [[path: 'target/allure-results']]
            }
        }
    }
}
