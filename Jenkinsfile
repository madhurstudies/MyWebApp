pipeline {
    agent any

    environment {
        // Change this to wherever you extracted Tomcat
        TOMCAT_WEBAPPS = 'C:\\apache-tomcat\\webapps'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Static site: "build" just verifies the page exists
                bat 'if not exist index.html (echo index.html missing & exit /b 1)'
                echo 'Build OK'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat 'if not exist "%TOMCAT_WEBAPPS%\\MyWebApp" mkdir "%TOMCAT_WEBAPPS%\\MyWebApp"'
                bat 'copy /Y index.html "%TOMCAT_WEBAPPS%\\MyWebApp\\"'
            }
        }
    }

    post {
        success {
            echo 'Deployed: http://localhost:8081/MyWebApp/'
        }
    }
}
