pipeline {
    agent any  // This will use a Windows agent if available

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning the repository using git...'
                // Use the git step to clone the repository
                git url: 'https://github.com/klsasank/QuizT.git', branch: 'main'
            }
        }

        stage('Build WAR') {
            steps {
                echo 'Building the WAR file...'
                // Use Windows batch commands to create the WAR file
                bat '''
                echo Cleaning up target directory
                rmdir /s /q target
                mkdir target
                echo Creating WAR file
                jar -cvf target/quizApp.war *
                '''
            }
        }

        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'bf987208-cbb1-40f1-aa8d-44145ac41c3a', path: '', url: 'http://localhost:8080')], contextPath: null, war: 'target/quizApp.war'
            }
        }
    }
}
