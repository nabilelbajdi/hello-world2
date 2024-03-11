'''
pipeline {
    agent any

    tools {
        jdk 'JDK'
        maven 'MAV'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}
'''
