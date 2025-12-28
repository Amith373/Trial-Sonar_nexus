pipeline {
    agent any


    environment {
        EC2_USER = "ubuntu"
        EC2_HOST = "3.110.193.167"
        JAR_NAME = "demo-0.0.1-SNAPSHOT.jar"
        APP_DIR  = "/home/ubuntu/app"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Amith373/Trial-Sonar_nexus.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mvn clean install
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying Application"

                sshagent(['ec2-ssh-key']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} 'mkdir -p ${APP_DIR}'
                        scp target/${JAR_NAME} ${EC2_USER}@${EC2_HOST}:${APP_DIR}/
                        ssh ${EC2_USER}@${EC2_HOST} 'nohup java -jar ${APP_DIR}/${JAR_NAME} > app.log 2>&1 &'
                    """
                }
            }
        }
    }
}
