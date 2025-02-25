pipeline {
    agent any
    
    /* Ваши инструкции */
    stages {
        // Извлекаем проект из репозитория 
        stage('Checkout') { 
            steps {
                echo 'Checkout'
            }
        }
        
        // Собираем проект. Получаем на выходе пакетный файл или билд 
        stage('Build') { 
            steps {
                echo 'Build'
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
