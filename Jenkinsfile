pipeline {
    agent any

    tools {
        nodejs "NodeJS_20" // name from Jenkins global config
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/manojvipl/Jenkins-Demo-Project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build & Run') {
            steps {
                sh 'npm start &'
            }
        }
    }

    post {
        success {
            echo '🎉 Build & Deploy Successful!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}

