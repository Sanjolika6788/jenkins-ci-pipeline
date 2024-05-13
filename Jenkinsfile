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
                    echo 'Building with Maven'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Run unit tests and integration tests using Maven
                    sh "${MAVEN_HOME}/bin/mvn test"
                    echo 'Running tests'
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
                    echo 'Analyzing code'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    // Example: Using OWASP Dependency Check
                    sh "${MAVEN_HOME}/bin/mvn org.owasp:dependency-check-maven:check"
                    echo 'Performing security scan'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    // Example deployment script to AWS EC2
                    sh 'deploy-to-staging.sh'
                    echo 'Deploying to AWS EC2 staging'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests in staging environment
                    sh 'run-staging-tests.sh'
                    echo 'Testing in staging'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy to production
                    sh 'deploy-to-production.sh'
                    echo 'Deploying to production server'
                }
            }
        }
    }
    post {
        always {
            emailext(
                to: 'ramukeka01@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName}",
                body: """\
                    Build finished with status: ${currentBuild.result}
                    Check console output at ${BUILD_URL} to view the results.
                    """,
                attachLog: true // Ensures the console log is attached
            )
        }
    }
}
