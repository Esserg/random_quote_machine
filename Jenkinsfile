pipeline {
    agent { node { label 'docker' } }
    
    environment {
        // Удобно вынести переменные, чтобы менять в одном месте
        REGISTRY = "192.168.10.80:8082"
        IMAGE_NAME = "random_quote_machine"
        DEPLOYMENT_NAME = "random-quote-machine"
    }
    
    /* Ваши инструкции */
    stages {
        // Извлекаем проект из репозитория 
        stage('Checkout') { 
            steps {
                git branch: 'main', url: 'https://github.com/Esserg/random_quote_machine.git'
            }
        }
        
        stage('Build') {
            steps {
                sh "docker build -t ${REGISTRY}/${IMAGE_NAME}:latest ."
                sh "docker push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }

        stage('Deploy') {
            steps {
                // 1. Применяем манифест (если были изменения в конфигах)
                sh 'kubectl apply -f deployment.yaml'
                
                // 2. Форсируем обновление подов, чтобы они перевыкачали образ latest
                sh "kubectl rollout restart deployment/${DEPLOYMENT_NAME}"
                
                // 3. (Опционально) Проверка статуса развертывания
                sh "kubectl rollout status deployment/${DEPLOYMENT_NAME}"
            }
        }
    }
}
