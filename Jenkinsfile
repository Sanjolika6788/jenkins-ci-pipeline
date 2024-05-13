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
                echo 'Running tests'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Testing in staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server'
            }
        }
    }
    post {
        always {
            emailext (
                to: 'ramukeka01@gmail.com',
                subject: "Build ${currentBuild.fullDisplayName}",
                body: """\
                    Build finished with status: ${currentBuild.result}
                    Check console output at ${BUILD_URL} to view the results.
                    """,
                attachLog: true  // Ensures the console log is attached
            )
        }
    }
}
