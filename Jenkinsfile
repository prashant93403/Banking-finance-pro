pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/prashant93403/Banking-finance-proj/', branch: "main"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t prashant910/staragileprojectfinance:1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push prashant910/staragileprojectfinance:1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-containe21210 -p 8084:80 prashant910/staragileprojectfinance:1'
                  
                }
            }
        
    }
}
