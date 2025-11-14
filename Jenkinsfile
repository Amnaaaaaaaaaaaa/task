pipeline {
    agent any

    stages {

        stage('Print Build Info') {
            steps {
                script {
                    echo "Build #${currentBuild.number}"
                    echo "Timestamp: ${new Date().format('yyyy-MM-dd HH:mm:ss')}"
                    if (currentBuild.getBuildCauses('org.jenkinsci.plugins.workflow.cps.CpsScmFlowDefinition$SCMTriggerCause').size() > 0) {
                        echo "Triggered by GitHub Webhook"
                    } else {
                        echo "Triggered manually"
                    }
                }
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Amnaaaaaaaaaaaa/task.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }
    }

    post {
        success {
            echo 'Build and tests successful!'
        }
        failure {
            echo 'Build failed or tests failed!'
        }
    }
}
