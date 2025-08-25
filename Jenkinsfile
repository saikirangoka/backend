pipeline {
    agent { label 'agent' }
    environment {
        PROJECT = 'expense'
        SERVICE = 'backend'
        ENVIRONMENT = 'QA'
        appVersion = ''
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