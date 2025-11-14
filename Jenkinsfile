pipeline {
    agent any

    stages {

        stage('Print Build Info') {
    steps {
        script {
            echo "Build #${env.BUILD_NUMBER}"
            echo "Timestamp: ${new Date()}"
            
            // Detect if triggered by GitHub webhook
            def causes = currentBuild.getBuildCauses()
            def triggeredByWebhook = false

            for (cause in causes) {
                if (cause.toString().contains("SCMTrigger") || cause.toString().contains("GitHubPushTrigger")) {
                    triggeredByWebhook = true
                    break
                }
            }

            if (triggeredByWebhook) {
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
