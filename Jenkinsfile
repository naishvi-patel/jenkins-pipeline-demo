pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * *') // Polls every 5 minutes
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running SonarQube Analysis...'
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Dependency-Check...'
                sh './dependency-check.sh --project JenkinsDemo --scan .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Replace with actual staging deployment steps
                sh 'scp target/*.jar user@staging-server:/opt/app'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Example: Postman Newman tests
                sh 'newman run tests/postman_collection.json'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Replace with actual production deployment steps
                sh 'scp target/*.jar user@production-server:/opt/app'
            }
        }
    }
}
