
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Creating virtual environment and installing dependencies'
                sh '''
                    python3 -m venv venv
                    venv/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests'
                sh 'venv/bin/python -m unittest discover -s .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
                sh '''
                    mkdir -p "$WORKSPACE/python-app-deploy"
                    cp app.py requirements.txt "$WORKSPACE/python-app-deploy/"
                '''
            }
        }

        stage('Run Application') {
            steps {
                echo 'Starting the deployed application'
                sh '''
                    cd "$WORKSPACE/python-app-deploy"
                    nohup "$WORKSPACE/venv/bin/python" app.py > app.log 2>&1 &
                    echo $! > app.pid
                '''
            }
        }

        stage('Test Application') {
            steps {
                echo 'Verifying the application'
                sh 'venv/bin/python test_app.py'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the Console Output.'
        }
    }
}
