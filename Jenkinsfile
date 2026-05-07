pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
            args '--user root'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/swethagandham2003/hybrid-qa-automation-ci-cd-framework.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python -m pip install --upgrade pip
                python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python -m pytest -n 4 --alluredir=allure-results'
            }
        }

        stage('Generate Report') {
            steps {
                sh '''
                apt-get update
                apt-get install -y default-jre
                wget https://github.com/allure-framework/allure2/releases/download/2.29.0/allure-2.29.0.tgz
                tar -xvzf allure-2.29.0.tgz
                ./allure-2.29.0/bin/allure generate allure-results -o allure-report --clean
                '''
            }
        }
    }
}
