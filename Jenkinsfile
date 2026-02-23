pipeline {
    agent any

    triggers {
        // every 5 minutes on Mondays
        cron('H/5 * * * 1')
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/3th34-Byte/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Test & JaCoCo') {
            steps {
                sh './mvnw test jacoco:report'
            }
        }

        stage('Publish JaCoCo') {
            steps {
                jacoco()
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
    }
}
