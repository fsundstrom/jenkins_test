pipeline {
   agent any

    // enverment var test
    environment { 
        def MYTESTSTR = 'testing 123'
    }

    stages {
        stage('Copy') {
            steps {
                echo 'copying..'
                // Get user and key from jenkins pram.
                sshagent (credentials: ['test200']) {
                   sh 'ssh -o StrictHostKeyChecking=no -l root buildservername ls -al'
                   sh 'ssh root@buildservername rm -rf /var/tmp/jenk_build'
                   sh 'ssh root@buildservername mkdir /var/tmp/jenk_build'
                   sh 'scp -r * root@buildservername:/var/tmp/jenk_build'
                 }
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                // enverment var test
                echo "Building ${env.MYTESTSTR} "
                // enverment var from jenkins pram test
                echo "Building ${env.TESTPRAM} "
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
                sshagent (credentials: ['test200']) {
                   sh 'ssh root@buildservername chmod 777 /var/tmp/jenk_build/test.sh'
                   sh 'ssh root@buildservername /var/tmp/jenk_build/test.sh'
                }
                }
        }
    }

    post('test') { 
          always { 
            cleanWs()
         }
   }
}

