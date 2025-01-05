pipeline{
    agent {
        label 'worker'
    }
    stages{
        stage("Build and Push"){
            steps{
                sh '''
                cd vote
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 503561443217.dkr.ecr.us-east-1.amazonaws.com
                docker build -t 503561443217.dkr.ecr.us-east-1.amazonaws.com/meenu-repo:vote .
                docker push 503561443217.dkr.ecr.us-east-1.amazonaws.com/meenu-repo:vote
                '''
            }
        }
        stage("Deploy"){
            steps{
                sh '''
                kubectl  set image deployment vote vote=503561443217.dkr.ecr.us-east-1.amazonaws.com/meenu-repo:vote
                kubectl rollout restart deployment vote
                '''
            }
        }
    }
}
