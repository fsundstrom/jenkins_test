pipeline {
   agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'ls -al'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh './test.sh||true'
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'scp test.sh root@192.168.1.223:/var/tmp'
                sh 'ssh root@192.168.1.223 chmod 777 /var/tmp/test.sh'
                sh 'ssh root@192.168.1.223 /var/tmp/test.sh'
            }
        }
    }
}

