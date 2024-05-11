pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building with Maven'
                // Example tool: Maven
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests'
                // Example tools: JUnit for unit tests, Selenium for integration tests
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code'
                // Example tool: SonarQube
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan'
                // Example tool: OWASP ZAP
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging'
                // Use a script or a Jenkins plugin compatible with AWS
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Testing in staging'
                // Tool: Postman for API testing
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server'
                // Use a script or a Jenkins plugin compatible with AWS
            }
        }
    }
    post {
        always {
            emailext(
                to: 'nonuchaudhary28@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName}",
                body: """\
                       Build finished with status: ${currentBuild.result}
                       Check console output at ${BUILD_URL} to view the results.
                       """,
                attachLog: true  // This will include the console log as an attachment
            )
        }
    }
}
