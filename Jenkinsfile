pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/local/apache-maven'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the application using Maven'
                    sh "${MAVEN_HOME}/bin/mvn clean package"
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests using JUnit and Mockito'
                    sh "${MAVEN_HOME}/bin/mvn test"
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code with SonarQube'
                    sh "${MAVEN_HOME}/bin/mvn sonar:sonar"
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan using OWASP ZAP'
                    sh 'zap-cli start'
                    sh 'zap-cli scan -t http://your-application-url'
                    sh 'zap-cli report -o security-report.html'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to AWS EC2 staging instance'
                    sh 'scp -i /path/to/key.pem ./target/myapp.war ec2-user@staging-instance:/var/www/html/'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging environment'
                    sh 'curl http://staging-instance-ip/test'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to AWS EC2 production instance'
                    sh 'scp -i /path/to/key.pem ./target/myapp.war ec2-user@production-instance:/var/www/html/'
                }
            }
        }
    }

    post {
        always {
            mail bcc: '', 
                 body: "A ${currentBuild.currentResult} occurred in the Jenkins pipeline stage.",
                 cc: '', 
                 from: 'ramukeka01@gmail.com', 
                 replyTo: '', 
                 subject: "Pipeline Notification: ${currentBuild.currentResult}", 
                 to: 'ramukeka01@gmail.com'
        }
    }
}
