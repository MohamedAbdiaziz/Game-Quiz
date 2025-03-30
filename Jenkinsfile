pipeline {
    agent any

    tools {
        nodejs 'Nodejs12'  // Use the Node.js installation you configured
    }

    environment {
        SONARQUBE_URL = 'SonarQubeServer'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
                script {
                    sh './your-build-script.sh' // Replace with your actual command to build or run the application
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Add testing commands (e.g., `sh 'mvn test'`)
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('SonarQubeServer') {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=Game-Quiz \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://your-sonarqube-server:9000 \
                        -Dsonar.qualitygate.wait=true
                        """
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    timeout(time: 5, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add deployment steps here
            }
        }
        
    }
}
