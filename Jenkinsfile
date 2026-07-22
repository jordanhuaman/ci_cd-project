pipeline {
    agent {
        docker {
            image 'oven/bun:1'
            args '-u root'
        }
    }

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'bun install --frozen-lockfile'
            }
        }

        stage('Lint') {
            steps {
                sh 'bun run lint || true' // quita el "|| true" si quieres que falle el build
            }
        }

        stage('Test') {
            steps {
                sh 'bun test'
            }
        }

        stage('Build') {
            steps {
                sh 'bun run build'
            }
        }
    }

    post {
        success {
            echo '✅ Build completado correctamente'
        }
        failure {
            echo '❌ El build falló'
        }
        always {
            cleanWs()
        }
    }
}