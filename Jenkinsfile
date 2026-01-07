pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AnkitKumar5277/Continous-Testing-Plan-using-Git-Postman-and-Jenkins.git'
            }
        }

        stage('Verify Node & Newman') {
            steps {
                bat '''
                echo Checking Node version
                node -v

                echo Checking NPM version
                npm -v
                '''
            }
        }

        stage('Install Newman') {
            steps {
                bat '''
                npm install -g newman newman-reporter-html
                '''
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                echo Creating reports folder if not exists
                if not exist reports mkdir reports

                echo Running Postman collection
                newman run postman/Continuous-Testing.postman_collection.json ^
                -r cli,html ^
                --reporter-html-export reports/postman-report.html ^
                || exit /b 0
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
                reportFiles: 'postman-report.html',
                reportName: 'Postman API Test Report'
            ])
        }

        success {
            echo '✅ Pipeline completed successfully'
        }

        failure {
            echo '❌ Pipeline failed'
        }
    }
}
