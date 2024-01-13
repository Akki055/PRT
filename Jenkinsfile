pipeline {
    agent none
    environment {
        DOCKERHUB_CREDENTIALS = credentials("e5a9fefd-0843-46d6-945f-d8ff286bf6c2")
    }
    stages {
        stage('git') {
            }
            steps {
                script {
                    git 'https://github.com/Akki055/PRT.git'
                }
            }
        }
        stage('docker') {
            }
            steps {
                script {
                    sh 'sudo docker C:\ProgramData\Jenkins\.jenkins\workspace\Proj/ -t akki058/proj2'
                    sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                    sh 'sudo docker push akki058/proj2'
                }
            }
        }
         stage('kubernetes') {
            agent {
                label "K8-master"
            }
            steps {
                script {
                    sh 'kubectl delete deploy nginx-deployment'
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl delete service my-service'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}
