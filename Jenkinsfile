pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/Amith373/Trial-Sonar_nexus.git'
            }
        }
        stage('build') {
            steps {
                echo "Building Application"
                sh '''
                   mvn clean package
                   '''
            }
        }
    }
}
