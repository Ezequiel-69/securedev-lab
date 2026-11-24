pipeline {
    agent any

    stages {
        stage('Construccion') {
            steps {
                sh 'docker build -t securedev-pipeline-test:latest .'
            }
        }
        stage('Pruebas') {
            steps {
                sh 'docker run --rm --network host -v $(pwd)/reports:/zap/wrk/:rw ghcr.io/zaproxy/zaproxy:stable zap-baseline.py -t http://127.0.0.1:8000 -r zap-pipeline.html || true'
            }
        }
        stage('Despliegue') {
            steps {
                sh 'docker ps --filter "name=securedev-lab-app" && curl -sf http://127.0.0.1:8000/health'
            }
        }
    }
}
