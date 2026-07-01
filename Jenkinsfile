pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Test') {
            steps {
                // Use 'package' to run tests AND create the jar file
                sh 'mvn clean package'
            }
        }
    }
    
    post {
        success {
            // Saves the jar into Jenkins build history
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        always {
            // Publishes test results
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
