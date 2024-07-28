pipeline {
    agent any

    tools {
        maven 'Maven' // Adjust as per your Maven version
        jdk 'JDK21' // Adjust as per your JDK version
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/your-repo-name.git'
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
