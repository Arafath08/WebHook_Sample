pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        APP_NAME = "sample-webhook-app"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning repository..."
                git branch: 'master', url: 'https://github.com/Arafath08/WebHook_Sample.git', credentialsId: 'github-credentials'
            }
        }

        stage('Debug') {
            steps {
                echo "Triggered by webhook for ${env.GIT_URL}"
            }
        }

        stage('Build') {
            steps {
                echo "Building the application..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests..."
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying build from Git commit ${GIT_COMMIT}"
                echo "Build successful for ${APP_NAME}"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
