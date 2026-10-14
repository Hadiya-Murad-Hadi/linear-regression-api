pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Deploy API') {
            steps {
                sh 'docker compose down --remove-orphans || true'
                sh 'docker rm -f linear-regression-api || true'
		sh 'docker compose pull'
		sh 'docker compose up -d'
            }
        }

        stage('Verify API') {
            steps {
                sh 'sleep 5'
                sh 'curl -f "http://localhost:5000/predict?x1=2&x2=3&x3=1"'
            }
        }
    }
}
