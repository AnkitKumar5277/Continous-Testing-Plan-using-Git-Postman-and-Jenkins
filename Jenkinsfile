pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/AnkitKumar5277/Continous-Testing-Plan-using-Git-Postman-and-Jenkins.git'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                newman run postman/Continuous-Testing.postman_collection.json ^
                -e postman/environment.json ^
                -r html --reporter-html-export reports/report.html
                '''
            }
        }
    }

    post {
        always {
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'reports',
                reportFiles: 'report.html',
                reportName: 'Postman API Test Report'
            ])
        }
    }
}
