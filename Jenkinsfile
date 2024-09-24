pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/Lakshya1997499/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t Lakshya1997499/9900814001/2feb .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push Lakshya1997499/9900814001/2feb'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 Lakshya1997499/9900814001/2feb'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 Lakshya1997499/9900814001/2feb"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.36.65 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.36.65 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
