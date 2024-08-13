pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/Nikky2608/Banking-java-project/'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with Nikky'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with Nikky'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa with Nikky'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with Nikky'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t nikhil268/project.v1 .'
           }
         }
        stage('Login to docker hub and push the file'){
            steps{
                withCredentials([string(credentialsId: 'dockerhubpass', variable: 'dockerhubpass')]) {
                    sh 'docker login -u nikhil268 -p ${dockerhubpass}'
                    sh 'docker push nikhil268/project.v1'
               }
            }
        }  
       stage{'Deployment stage using ansible'}{
           steps{
               ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml', sudoUser: null, vaultTmpPath: ''
            }
        }
    }
 }
}
