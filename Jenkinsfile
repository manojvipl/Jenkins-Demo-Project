pipeline {
    agent any

    tools {
        nodejs "NodeJS_20"
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

        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy Locally') {
            steps {
                script {
                    echo "Deploying NodeJS App on same EC2 server..."
                    // Stop any existing process running on port 3000 (optional)
                    sh 'pm2 delete jenkins-demo || true'
                    // Start app using PM2
                    sh 'pm2 start server.js --name jenkins-demo'
                    // Save PM2 list so app auto-starts after reboot
                    sh 'pm2 save'
                }
            }
        }
    }
}

