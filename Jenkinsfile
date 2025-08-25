pipeline {
    agent { label 'agent' }
    environment {
        PROJECT = 'expense'
        SERVICE = 'backend'
        ENVIRONMENT = 'QA'
        appVersion = ''
        ACCOUNT_NUMBER = '412306530000'
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }
    stages {
        stage('Read version'){
            steps {
                script {
                    def packagejson = readJSON file: 'package.json'
                    appVersion = packagejson.version
                    echo "version is: $appVersion"
                }
            }
        }
        stage('install dependencies') {
            steps {
                script {
                    sh """
                        npm install
                    """
                }
            }
        }
        stage('docker') {
            steps {
                script {
                    withAWS(region: 'us-east-1', credentials: 'aws-creds') {
                    sh """
                        aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACCOUNT_NUMBER}.dkr.ecr.us-east-1.amazonaws.com
                        docker build -t ${ACCOUNT_NUMBER}.dkr.ecr.us-east-1.amazonaws.com/expense/backend:appVersion .
                        docker push ${ACCOUNT_NUMBER}.dkr.ecr.us-east-1.amazonaws.com/expense/backend:appVersion
                    """
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'always shows '
            deleteDir()
        }
        failure {
            echo 'failure occurs'
        }
        success {
            echo 'success occurs'
        }
    }
}


// pipeline {
//     agent any
//     stages {
//         stage('Build') {
//             steps {
//                 //
//             }
//         }
//         stage('Test') {
//             steps {
//                 //
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 //
//             }
//         }
//     }
// }