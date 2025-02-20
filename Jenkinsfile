pipeline {
    agent any

    environment {
        SKIP_CRASH = "true"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JennyZhang2022/spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package'
            }
        }
        
        stage('Test & Code Coverage') {
            steps {
                sh './mvnw test -Dtest=!CrashControllerTests'
                sh './mvnw jacoco:report'
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    
    triggers {
        cron('H/10 * * * 1')
    }
}
