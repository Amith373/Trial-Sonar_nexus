pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME=tool 'sonar'
    }
    stages {
        stage('git checkout') {
            steps {
              git branch: 'main', url: 'https://github.com/Amith373/Trial-Sonar_nexus.git'
            }
        }
        stage('complie code') {
            steps {
              sh "mvc clean compile"
            }
        }
        stage('code test') {
            steps {
              sh "mvc test"
            }
        }
        stage('sonar analsus') {
            steps {
                 withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=sonar-qube-analsys \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=sonar-qube-analsys '''
             }
        }
    }
}
