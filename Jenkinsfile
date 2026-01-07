pipeline {
    agent any

    tools {
        allure 'Allure'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: '<your-repo-url>'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                newman run postman/Continuous-Testing.postman_collection.json ^
                -e postman/environment.json ^
                -r allure ^
                --reporter-allure-export allure-results
                '''
            }
        }
    }

    post {
        always {
            allure([
                includeProperties: false,
                jdk: '',
                results: [[path: 'allure-results']]
            ])
        }
    }
}

