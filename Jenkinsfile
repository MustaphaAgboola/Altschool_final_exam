pipeline {
    agent any

    environment {
        devs = "dev-server"
    }

    // stages {
    //     stage('Nginx Deployment and mongoDB') {
    //         steps {
    //             sshagent(['Admin1_SSH_Private_Key']){
    //                 sh "scp -o strictHostKeyChecking=no deployment.yaml ec2-user@3.87.127.237:/home/ec2-user"
    //                 sh "scp -o strictHostKeyChecking=no secret.yml ec2-user@3.87.127.237:/home/ec2-user"
    //                 sh "scp -o strictHostKeyChecking=no configMapMongodb.yml ec2-user@3.87.127.237:/home/ec2-user"
    //                 sh "scp -o strictHostKeyChecking=no mongo.yaml ec2-user@3.87.127.237:/home/ec2-user"
    //                 sh "scp -o strictHostKeyChecking=no mongoExpress.yml ec2-user@3.87.127.237:/home/ec2-user"
    //                 script {
    //                     try{
    //                         sh "ssh ec2-user@3.87.127.237 kubectl create -f deployment.yaml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl create -f secret.yml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl create -f configMapMongodb.yml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl create -f mongo.yaml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl create -f mongoExpress.yml"
    //                     }catch(error) {
    //                         sh "ssh ec2-user@3.87.127.237 kubectl apply -f deployment.yaml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl apply -f secret.yml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl apply -f configMapMongodb.yml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl apply -f mongo.yaml"
    //                         sh "ssh ec2-user@3.87.127.237 kubectl apply -f mongoExpress.yml"
    //                     }
    //                 }
    //             }
    //         }
    //     }
        stage('git clone socks app') {
            steps {
                git branch: 'master', url: 'https://github.com/Steveric1/microservices-demo.git'
            }
        }
        stage('Socks App Deployment'){
            steps {
                dir('deploy/kubernetes') {
                    sshagent(['Admin1_SSH_Private_Key']) {
                        sh "scp -o strictHostKeyChecking=no complete-demo.yaml ec2-user@18.209.173.23:/home/ec2-user"
                        script {
                            try {
                                sh "ssh ec2-user@18.209.173.23 kubectl create -f complete-demo.yaml"
                            } catch(error) {
                                sh "ssh ec2-user@18.209.173.23 kubectl apply -f complete-demo.yaml"
                            }
                        }
                    }
                }
            }
        }
    }
}