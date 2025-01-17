pipeline {
    agent any
    environment{
        WORKSPACE = "C:\\AdityaPersonal\\nexTurn\\AdityaSharma_NexTurn_Assignments\\M6_Jenkins_Assignments\\Exercise_2\\vite-project"
    }
    stages {
        stage('Changing Directory') {
            steps {
                script {
                    echo "Changing Directory.."
                    cd @env.WORKSPACE
                }
            }
        }
        stage('Installing Dependencies') {
            steps {
                script {
                    echo "Installing Dependencies.."
                    npm install
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    echo "Running Tests.."
                    npm test
                }
            }
        }
        stage('Build Project') {
            steps {
                script {
                    echo "Building the project.."
                    npm run build
                }
            }
        }
        stage('Deployment Directory') {
            steps {
                script {
                    echo "Deploying the application by copying the build folder to a deployment directory..."
                    xcopy @env.WORKSPACE\dist @env.WORKSPACE\deployment-directory /E /I /H /Y 
                }
            }
        }
    }
    post {
        always {
            echo "Archiving Reports"
            archiveArtifacts artifacts: 'reports/*.xml, reports/*.html', fingerprint: true
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'reports',
                reportFiles: 'report.html',
                reportName: 'Test Report'
            ])
        }
    }
}