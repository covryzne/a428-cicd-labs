pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
                        sh 'npm install'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
                        sh './jenkins/scripts/test.sh'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
                        sh './jenkins/scripts/deliver.sh'
                        input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                        sh './jenkins/scripts/kill.sh'
                    }
                }
            }
        }
    }
}