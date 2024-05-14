pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building with Maven'
                // To actually build with Maven, you would use a step like: sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit and integration tests with Selenium'
                // You might include actual commands here to run tests
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
                // You might include a step like: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP ZAP'
                // To actually scan with OWASP ZAP, you would use a step like: sh 'zap-cli start'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging'
                // To deploy, you might use a step like: sh 'deploy-script.sh staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging with Postman'
                // You might use a step to trigger Postman tests here
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server on AWS EC2'
                // To deploy, you might use a step like: sh 'deploy-script.sh production'
            }
        }
    }
    post {
        failure {
            emailext(
                to: 'nonuchaudhary28@gmail.com',
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
                to: 'nonuchaudhary28@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName} Succeeded",
                body: """\
                       Build succeeded with status: ${currentBuild.result}
                       Check console output at ${BUILD_URL} to view the results.
                       """,
                attachLog: true
            )
        }
        always {
            emailext(
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                       <p>Status: ${currentBuild.currentResult}</p>
                       <p>Check console output at <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>""",
                to: 'nonuchaudhary28@gmail.com'
            )
        }
    }
}
