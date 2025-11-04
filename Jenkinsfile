pipeline {
    agent any
    environment {
        VIRTUAL_ENV = 'venv'
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    if (!fileExists("${env.WORKSPACE}\\${VIRTUAL_ENV}")) {
                        powershell "python -m venv ${VIRTUAL_ENV}"
                    }
                    powershell """
                        & ${VIRTUAL_ENV}\\Scripts\\Activate.ps1
                        pip install -r requirements.txt
                    """
                }
            }
        }
        stage('Lint') {
            steps {
                script {
                    powershell """
                        & ${VIRTUAL_ENV}\\Scripts\\Activate.ps1
                        flake8 app.py
                    """
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    powershell """
                        & ${VIRTUAL_ENV}\\Scripts\\Activate.ps1
                        pytest
                    """
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying application...'
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
