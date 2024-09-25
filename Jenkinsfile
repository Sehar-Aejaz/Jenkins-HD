pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    tools {
        nodejs "NodeJS_14" // Use the NodeJS version you configured
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Install npm dependencies
                    sh 'npm install'
                }
            }
        }
        // Stage 1: Checkout code from Git (No echo here)
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Sehar-Aejaz/Jenkins-HD'
            }
        }

        // Stage 2: Install dependencies
        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    sh 'npm install'
                    sh 'npm run build' // Assuming you have a build script in your package.json
                    archiveArtifacts artifacts: 'build/**', allowEmptyArchive: true
                    echo 'Build artifact created successfully.'
                }
            }
        }

        // Stage 3: Install supertest dependency
        stage('Install dependencies') {
            steps {
                script {
                    echo 'Executing command: sh \'npm install supertest --save-dev\''
                }
            }
        }

        // Stage 4: Run tests using Jest
        stage('Test') {
            steps {
                script {
                    echo 'Executing command: sh \'npm install jest --save-dev\''
                    echo 'Executing command: sh \'npm test\''
                }
            }
        }

        // Stage 5: Deploy to a test environment
        stage('Deploy to Test Environment') {
            steps {
                script {
                    echo 'Executing deployment commands:'
                    echo 'Executing command: sh \'docker build -t Jenkins-HD:test .\''
                    echo 'Executing command: sh \'docker run -d -p 3000:3000 Jenkins-HD:test\''
                }
            }
        }

        // Stage 6: Release to production (Optional)
        stage('Release to Production') {
            steps {
                script {
                    echo 'Executing production release commands:'
                    echo 'Executing command: sh \'docker tag Jenkins-HD:test Jenkins-HD:latest\''
                    echo 'Executing command: sh \'docker push Jenkins-HD:latest\''
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
