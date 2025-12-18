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
        stage('dependancy check') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --format HTML ', odcInstallation: 'DC'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('Docker build & push') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-login', url: 'https://index.docker.io/v1/') {
                sh "docker build -t image1 ."
                sh "docker tag image1 manlineroot12/springboot-sonarqube-test:v1 "
                sh "docker push manlineroot12/springboot-sonarqube-test:v1"
                }
            }
        }
        stage('Trivy scan') {
            steps {
                sh "trivy --timeout 20m image manlineroot12/springboot-sonarqube-test:v1"
            }
        }
        stage("Deploy To Tomcat"){
            steps{
                sh "cp /var/lib/jenkins/.m2/repository/com/example/demo/0.0.1-SNAPSHOT/demo-0.0.1-SNAPSHOT.war /opt/apache-tomcat-9.0.65/webapps/ "
            }
        }
    }
}
