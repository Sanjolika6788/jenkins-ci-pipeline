pipeline {
    agent any

    tools {
        // Define Maven tool configured in Jenkins
        maven 'Maven_3.8.1' // Ensure to replace 'Maven_3.8.1' with the actual name of your configured Maven in Jenkins
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                script {
                    try {
                        sh 'mvn clean install'
                    } catch (Exception e) {
                        error "Build failed. ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                script {
                    try {
                        sh 'mvn test'
                    } catch (Exception e) {
                        error "Tests failed. ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                script {
                    try {
                        sh 'mvn sonar:sonar'
                    } catch (Exception e) {
                        error "Code analysis failed. ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                script {
                    try {
                        powershell './runSecurityScan.ps1'
                    } catch (Exception e) {
                        error "Security scan failed. ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 Staging...'
                script {
                    try {
                        powershell './deployStaging.ps1'
                    } catch (Exception e) {
                        error "Staging deployment failed. ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                script {
                    try {
                        powershell 'Invoke-WebRequest -Uri http://staging-server/test-suite'
                    } catch (Exception e) {
                        error "Integration tests on staging failed. ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 Production...'
                script {
                    try {
                        powershell './deployProduction.ps1'
                    } catch (Exception e) {
                        error "Production deployment failed. ${e.getMessage()}"
                    }
                }
            }
        }
    }
    
    post {
        always {
            emailext (
                to: 'ramukeka01@gmail.com',
                subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.result}",
                body: """<p>See attached logs and results for details.</p>
                         <p>Build: ${env.BUILD_URL}</p>""",
                attachmentsPattern: '**/*.log',
                mimeType: 'text/html'
            )
        }
        failure {
            echo 'Notifying failure...'
            emailext (
                to: 'ramukeka01@gmail.com',
                subject: "Failed: Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.result}",
                body: """<p>Failure occurred. Please check the Jenkins console for more details.</p>
                         <p>Build: ${env.BUILD_URL}</p>""",
                mimeType: 'text/html'
            )
        }
    }
}
