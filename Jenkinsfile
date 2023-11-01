pipeline{
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub1')
    }
    stages{
        stage("Clone the Code"){
            steps{
                git url:"https://github.com/aditi-orpe/ang-demo2.git",branch:"main"
            }
            
        }
        stage("Build"){
            steps{
                sh "docker build -t ang-demo2 ."
            }
        }
        stage("Push to docker hub"){
            steps{
                echo "$DOCKERHUB_CREDENTIALS_USR"
                sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                sh "docker tag ang-demo2 aditiorpe/ang-demo2:latest"
                sh "docker push aditiorpe/ang-demo2:latest"
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploy"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}
