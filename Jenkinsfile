pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/CletusLee/java-maven-junit-helloworld'
            }
        }
        stage('Clean Workspace') {
            agent {docker 'maven:3.5.3-jdk-8'}
            steps {
                sh 'mvn clean'
            }
        }
        stage('Build') {
            agent {docker 'maven:3.5.3-jdk-8'}
            steps {
                sh 'mvn package'
            }
        }
        stage('Publish Reports') {
            steps {
                 publishHTML([allowMissing: true, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'target/site/jacoco/', reportFiles: 'index.html', reportName: 'Code Coverage', reportTitles: ''])
                 junit 'target/surefire-reports/TEST-*.xml'
            }
        }
    }
}