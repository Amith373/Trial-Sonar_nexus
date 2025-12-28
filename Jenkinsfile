pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/Amith373/Trial-Sonar_nexus.git'
            }
        }
    stage('deploy') {
            steps {
                echo "Deploying Application"
                sh '''
                   nohup java -jar demo-0.0.1-SNAPSHOT.jar &
                   '''
            }
        }

        
    }
}
