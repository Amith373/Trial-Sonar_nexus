pipeline {
    agent any

    tools{
        maven 'Maven3'
        jdk 'JDK11'
      }

    environoment{
        EC2_USER = "ubuntu"
        EC2_HOST = "3.110.193.167"
        JAR_NAME = "demo-0.0.1-SNAPSHOT.jar"

    stages {
        stage('checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/Amith373/Trial-Sonar_nexus.git'
            }
        }
     stages {
        stage('build') {
            steps {
               sh '''
               mvn clean install
               '''
            }
        }
    stage('deploy') {
            steps {
                echo "Deploying Application" 
                sshagent(['ec2-ssh-key']) {

                    sh """
                    scp target/${JAR_NAME} ${EC2_USER}@${EC2_HOST}:${APP_DIR}
                    nohup java -jar ${JAR_NAME} &
                    

            }
        }        
    }
}
