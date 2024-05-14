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
            emailext(
                to: 'ramukeka01@gmail.com',
                subject: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} Status: ${currentBuild.currentResult}",
                body: """\
                    Build finished with status: ${currentBuild.currentResult}
                    Check console output at ${env.BUILD_URL} to view the results.
                    """,
                attachLog: true
            )
        }
    }
}
