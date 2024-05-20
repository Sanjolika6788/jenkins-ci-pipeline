pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building with Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit and integration tests with Selenium'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP ZAP'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging with Postman'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server on AWS EC2'
            }
        }
    }
    post {
        failure {
            emailext(
                to: 'ramukeka01@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName} Failed",
                body: """\
                       <p>Build failed with status: ${currentBuild.result}</p>
                       <p>Check console output at <a href="${env.BUILD_URL}">${env.BUILD_URL}</a> to view the results.</p>
                       """,
                attachLog: true
            )
        }
        success {
            emailext(
                to: 'ramukeka01@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName} Succeeded",
                body: """\
                       <p>Build succeeded with status: ${currentBuild.result}</p>
                       <p>Check console output at <a href="${env.BUILD_URL}">${env.BUILD_URL}</a> to view the results.</p>
                       """,
                attachLog: true
            )
        }
        always {
            emailext(
                to: 'ramukeka01@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """\
                       <p>Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                       <p>Status: ${currentBuild.currentResult}</p>
                       <p>Check console output at <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                       """,
                attachLog: true
            )
        }
    }
}
