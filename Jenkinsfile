pipeline {
    agent any

    environment {
            EC2-USER = "ubuntu"
            EC2-HOST = "3.110.193.167"
    }
    stages {
        stage('checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/Amith373/Trial-Sonar_nexus.git'
            }
        }
    stage('deploy') {
            steps {
                echo "Deploying Application"
                sshagent(['ec2-ssh-key']) {
                sh '''
                   nohup java -jar demo-0.0.1-SNAPSHOT.jar &
                   '''
            }
        }        
    }
}
