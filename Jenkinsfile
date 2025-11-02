pipeline {
    agent any

    tools {
        maven 'Maven-3.9.9'
        jdk 'JDK-21'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // If using local folder, skip this and Jenkins will use your workspace files.
                // If using GitHub, uncomment below and replace URL.
                // git branch: 'main', url: 'https://github.com/yourusername/maven-pipeline-demo.git'
                echo 'Using local workspace code...'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-creds', path: '', url: 'http://localhost:8080')],
                    contextPath: 'mavenapp',
                    war: 'target/*.war'
            }
        }
    }
}
