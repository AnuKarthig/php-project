pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/AnuKarthig/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t anukarthig/akshatnewimg6july:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push anukarthig/akshatnewimg6july:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 anukarthig/akshatnewimg6july:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 anukarthig/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.87.175 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.87.175 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
