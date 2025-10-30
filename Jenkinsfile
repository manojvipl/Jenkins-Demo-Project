pipeline {
    agent any

    tools {
        nodejs "NodeJS_20"
    }

    environment {
        DEPLOY_SERVER = "ubuntu@13.218.141.9"
        APP_DIR = "/root/jenkins-nodejs-demo"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/manojvipl/Jenkins-Demo-Project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Application') {
            steps {
                sh 'npm run build || echo "No build step configured"'
            }
        }

        stage('Deploy to EC2 Server') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no $DEPLOY_SERVER '
                            cd $APP_DIR &&
                            git pull &&
                            npm install &&
                            pm2 restart my-app || pm2 start app.js --name my-app
                        '
                    """
                }
            }
        }
    }
}

