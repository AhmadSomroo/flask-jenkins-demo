pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AhmadSomroo/flask-jenkins-demo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest
                '''
            }
        }

        stage('Build Application') {
            steps {
                sh '''
                    mkdir -p build
                    cp app.py build/
                    cp requirements.txt build/
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    mkdir -p /tmp/flask_deploy
                    cp -r build/* /tmp/flask_deploy/
                    echo "Application deployed successfully"
                '''
            }
        }
    }
}
