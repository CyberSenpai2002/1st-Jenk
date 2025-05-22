pipeline {
    agent any

    environment {
        IMAGE_NAME = 'cybersenpai/1stjenk' 
        IMAGE_TAG = "latest"
        DOCKERHUB_CREDS = credentials('dockerhub-creds')
    }

    stages {
        stage('Сборка Docker-образа') {
            steps {
                echo "Собираем Docker-образ..."
                sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
            }
        }

        stage('Логин в DockerHub') {
            steps {
                echo 'Выполняем логин...'
                sh "echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin"
            }
        }

        stage('Push в DockerHub') {
            steps {
                echo "Пушим образ..."
                sh "docker push $IMAGE_NAME:$IMAGE_TAG"
            }
        }
    }
}
