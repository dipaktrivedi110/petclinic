pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning petclinic repo...'
                git branch: 'main', url: 'https://github.com/dipaktrivedi110/petclinic.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploy') {
            steps {
                echo '✅ Application build and ready to deploy (simulated)'
            }
        }
    }
}

