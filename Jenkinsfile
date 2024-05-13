pipeline {
    agent any
    environment {
        MAVEN_HOME = '/path/to/maven'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Use Maven to compile and package the application
                    sh "${MAVEN_HOME}/bin/mvn clean package"
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Run unit tests and integration tests using Maven
                    sh "${MAVEN_HOME}/bin/mvn test"
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' // Collect JUnit test reports
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    // Analyze code using SonarQube
                    sh "${MAVEN_HOME}/bin/mvn sonar:sonar"
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    // Example: Using OWASP Dependency Check
                    sh "${MAVEN_HOME}/bin/mvn org.owasp:dependency-check-maven:check"
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    // Example deployment script to AWS EC2
                    sh 'deploy-to-staging.sh'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests in staging environment
                    sh 'run-staging-tests.sh'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy to production
                    sh 'deploy-to-production.sh'
                }
            }
        }
    }
    post {
        always {
            // Send email notifications
            emailext(
              subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
              body: """<p>Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                       <p>Status: ${currentBuild.currentResult}</p>
                       <p>Check console output at <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>""",
              to: 'ramukeka01@gmail.com'
            )
        }
    }
}
