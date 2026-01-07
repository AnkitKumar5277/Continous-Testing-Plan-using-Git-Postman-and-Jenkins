pipeline {
    agent any

    tools {
        nodejs 'NodeJS'   // Configure NodeJS in Jenkins Global Tools
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AnkitKumar5277/Continous-Testing-Plan-using-Git-Postman-and-Jenkins.git'
            }
        }

        stage('Install Newman') {
            steps {
                bat 'npm install -g newman newman-reporter-html'
            }
        }

        stage('Run Postman Collection') {
            steps {
                bat '''
                newman run postman/Continuous-Testing.postman_collection.json ^
                -r cli,html ^
                --reporter-html-export reports/postman-report.html
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'reports/*.html', fingerprint: true
        }

        success {
            echo '✅ Postman tests executed successfully!'
        }

        failure {
            echo '❌ Postman tests failed. Please check the report.'
        }
    }
}
