pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                // Example command: sh 'mvn clean install'
            }
            post {
                always {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Build Stage: ${currentBuild.fullDisplayName}",
                         body: "The build stage has completed. Please check the logs for details.",
                         attachmentsPattern: '**/target/*.log'
                }
                failure {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Build Stage Failed: ${currentBuild.fullDisplayName}",
                         body: "The build stage has failed. Please check the logs for details.",
                         attachmentsPattern: '**/target/*.log'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration tests using JUnit...'
                
            }
            post {
                always {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Unit and Integration Tests: ${currentBuild.fullDisplayName}",
                         body: "The tests have completed. Please check the logs for details.",
                         attachmentsPattern: '**/target/test-results/*.log'
                }
                failure {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Tests Failed: ${currentBuild.fullDisplayName}",
                         body: "The tests have failed. Please check the logs for details.",
                         attachmentsPattern: '**/target/test-results/*.log'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube...'
                // Example command: sh 'sonar-scanner'
            }
            post {
                always {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Code Analysis: ${currentBuild.fullDisplayName}",
                         body: "Code analysis has completed. Please check the logs for details.",
                         attachmentsPattern: '**/target/sonar/*.log'
                }
                failure {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Code Analysis Failed: ${currentBuild.fullDisplayName}",
                         body: "Code analysis failed. Please check the logs for details.",
                         attachmentsPattern: '**/target/sonar/*.log'
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scan using OWASP Dependency Check...'
                
            }
            post {
                always {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Security Scan: ${currentBuild.fullDisplayName}",
                         body: "Security scan has completed. Please check the logs for details.",
                         attachmentsPattern: '**/target/security/*.log'
                }
                failure {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Security Scan Failed: ${currentBuild.fullDisplayName}",
                         body: "Security scan failed. Please check the logs for details.",
                         attachmentsPattern: '**/target/security/*.log'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging server...'
                // Example command: sh './deploy.sh staging'
            }
            post {
                always {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Deployment to Staging: ${currentBuild.fullDisplayName}",
                         body: "Deployment to staging server completed. Please check the logs for details.",
                         attachmentsPattern: '**/target/deploy/*.log'
                }
                failure {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Deployment to Staging Failed: ${currentBuild.fullDisplayName}",
                         body: "Deployment to staging failed. Please check the logs for details.",
                         attachmentsPattern: '**/target/deploy/*.log'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on Staging environment...'
                // Integration testing commands
            }
            post {
                always {
                    mail to: 'gaveengt@gmail.com',
                         subject: "Integration Tests on Staging: ${currentBuild.fullDisplayName}",
                         body: "Integration tests on staging completed. Please check the logs for details.",
                         attachmentsPattern: '**/target/staging-tests/*.log'
                }
