pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                powershell 'mvn clean install'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                powershell 'mvn test'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
                }
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
            emailext (
                to: 'email@example.com',
                subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.result}",
                body: """<p>See attached logs and results for details.</p>
                         <p>Build: ${env.BUILD_URL}</p>""",
                attachmentsPattern: '**/*.log',
                mimeType: 'text/html'
            )
        }
    }
}
