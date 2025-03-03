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
                sh 'docker build -t 192.168.10.20:5000/random_quote_machine:0.$BUILD_ID'
                sh 'docker push 192.168.10.20:5000/random_quote_machine:0.$BUILD_ID'
            }
        }

        // Загружаем архив с проектом на удаленный сервер
        stage('Deploy') { 
            steps {
                echo 'Deploy'
            }
        }
    }
}
