pipeline {
    agent { node { label 'docker' } } 
    
    /* Ваши инструкции */
    stages {
        // Извлекаем проект из репозитория 
        stage('Checkout') { 
            steps {
                git branch: 'main', url: 'https://github.com/Esserg/random_quote_machine.git'
            }
        }
        
        // Собираем проект. Получаем на выходе пакетный файл или билд 
        stage('Build') { 
            steps {
                sh 'docker build -t 192.168.10.20:5000/random_quote_machine:test .'
                sh 'docker push 192.168.10.20:5000/random_quote_machine:test'
            }
        }

        // Загружаем архив с проектом на удаленный сервер
        stage('Deploy') { 
            steps {
                echo 'Deploy'
                curl -I https://192.168.10.20:9443/api/webhooks/88f69f4f-c39d-4353-ad7b-997db4c01af8
            }
        }
    }
}
