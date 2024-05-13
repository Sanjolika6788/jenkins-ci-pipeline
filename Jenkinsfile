pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                powershell 'mvn clean install'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                powershell 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                powershell 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                powershell './runSecurityScan.ps1' // Assumes a PowerShell script for security scanning
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 Staging...'
                powershell './deployStaging.ps1' // Assumes a PowerShell deployment script
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                powershell 'Invoke-WebRequest -Uri http://staging-server/test-suite' // Example command
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 Production...'
                powershell './deployProduction.ps1' // Assumes a PowerShell deployment script
            }
        }
    }
    
    post {
        always {
            mail to: 'princerani27@gmail.com',
                 subject: "Pipeline ${currentBuild.fullDisplayName} ${currentBuild.result}",
                 body: "See attachments for logs and results.",
                 attachmentsPattern: "**/*.log"
        }
    }
}
