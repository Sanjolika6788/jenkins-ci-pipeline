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
                echo 'Running unit tests with JUnit and integration tests with Selenium'
                // Example tools: JUnit for unit tests, Selenium for integration tests
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
                // Example tool: SonarQube
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP ZAP'
                // Example tool: OWASP ZAP
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging'
                // Deployment to AWS EC2 staging
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging with Postman'
                // Tool: Postman for API testing
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server on AWS EC2'
                // Deployment to AWS EC2 production
            }
        }
    }
    post {
        failure {
            emailext(
                to: 'ramukeka01@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName} Failed",
                body: """\
                       Build failed with status: ${currentBuild.result}
                       Check console output at ${BUILD_URL} to view the results.
                       """,
                attachLog: true
            )
        }
        success {
            emailext(
                to: 'ramukeka01@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName} Succeeded",
                body: """\
                       Build succeeded with status: ${currentBuild.result}
                       Check console output at ${BUILD_URL} to view the results.
                       """,
                attachLog: true
            )
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
    }
}
