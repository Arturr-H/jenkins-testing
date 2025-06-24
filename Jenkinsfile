pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                PYTHONPATH=$PWD bash -c "
                source venv/bin/activate
                pytest tests/
                "
                '''
            }
        }

        stage('Run App') {
            steps {
                sh '. venv/bin/activate && python app.py'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
