pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build (Java 17)') {
            steps {
                // This tells the Jenkins container to run the build inside your 'java17-builder' container
                sh 'docker exec java17-builder ./mvnw clean compile'
            }
        }

        stage('Run Unit Tests (Java 11)') {
            steps {
                sh 'docker exec java11-tester ./mvnw test'
            }
        }

        stage('Code Analysis (Java 8)') {
            steps {
                echo 'Skipping SonarQube for this run to ensure build works first...'
                // sh 'docker exec java8-analyzer ./mvnw sonar:sonar'
            }
        }
    }
}
