pipeline {
    agent any  // Use any available agent

    environment {
        MAVEN_HOME = tool 'Maven'  // Ensure Maven is installed in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/harishbitcse82/MyMavenApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'  // Run unit tests
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.projectKey=your-project-key'
            }
        }

        stage('Deploy') {
            steps {
                sh 'mvn deploy'  // Deploy to repository (e.g., Nexus, Artifactory)
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

