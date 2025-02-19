pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1') // This triggers the build every 10 minutes on Mondays
    }

    tools {
        jdk 'jdk11'
        maven 'Maven 3'
    }

    environment {
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'mvn clean install -DskipTests=true'
                }
            }
        }

        stage('Test and Generate JaCoCo Report') {
            steps {
                script {
                    sh 'mvn test jacoco:report'
                }
            }
        }

        stage('Publish JaCoCo Report') {
            steps {
                archiveArtifacts allowEmptyArchive: true, artifacts: '**/target/site/jacoco/*.html'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
