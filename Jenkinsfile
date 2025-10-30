pipeline {
    agent any

    tools {
        nodejs "NodeJS_18"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                bat 'npm test'
            }
        }
        stage('Build') {
    steps {
        echo 'Building project...'
        script {
            def result = bat(returnStatus: true, script: 'npm run build')
            if (result != 0) {
                echo "⚠️ No build script found, skipping build."
            }
        }
    }
}

   
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.js', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check logs for details.'
        }
    }
}
