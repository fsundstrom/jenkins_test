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
                sh '.\\test.sh||true'
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

