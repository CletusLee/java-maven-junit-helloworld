pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/CletusLee/java-maven-junit-helloworld'
            }
        }
        stage('Build') {
            agent {docker 'maven:3.5.3-jdk-8'}
            steps {
                sh 'mvn clean package'
                publishHTML([allowMissing: true, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'target/site/jacoco/', reportFiles: 'index.html', reportName: 'Code Coverage', reportTitles: ''])
                junit 'target/surefire-reports/TEST-*.xml'
            }
        }
    }
}