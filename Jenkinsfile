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
                echo 'Deploying to EC2...'
                script {
                    def ec2_user = "ubuntu"
                    def ec2_host = "3.80.21.217"
                    def jar_name = "petclinic-1.0-SNAPSHOT.jar"
                    def pem_key = "/var/lib/jenkins/.ssh/id_rsa"

                    // Copy JAR to EC2
                    sh """
                        scp -i ${pem_key} target/${jar_name} ${ec2_user}@${ec2_host}:/home/${ec2_user}/
                    """

                    // SSH into EC2 and run the JAR
                    sh """
                        ssh -i ${pem_key} ${ec2_user}@${ec2_host} 'nohup java -jar /home/${ec2_user}/${jar_name} > /home/${ec2_user}/petclinic.log 2>&1 &'
                    """
                }
            }
        }
    }
}

