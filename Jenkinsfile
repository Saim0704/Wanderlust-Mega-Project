@Library('shared') _
pipeline {
    agent any
    environment {
    // GIT
        GIT_REPO_URL = "https://github.com/Saim0704/Wanderlust-Mega-Project.git"
        GIT_BRANCH = "main"
        DOCKER_USER_NAME = "saim0704"
        REPO_NAME = "wanderlust-frontend"
    // Sonar_Qube
        SCANNER_HOME=tool "sonar"
        SONARQUBE_SERVER = "sonar"
        SONAR_TOKEN = "sonar-scanner-token"
        PROJECT_NAME = "Wanderlust-Frontend"
        PROJECT_KEY = "Wanderlust-Frontend"
    // Docker
        DOCKER_CRED_ID = "docker_token"
        TYPE = "frontend"
    }

    stages {
        stage('Clone') {
            steps {
                script{
                    git_checkout("${env.GIT_REPO_URL}", "${env.GIT_BRANCH}")
                }
            }
        }
        stage('Sonar Scanner') {
            steps {
                dir("${env.TYPE}"){
                    sonar_scanner("${env.SONARQUBE_SERVER}", "${env.PROJECT_NAME}", "${env.PROJECT_KEY}")
                }
            }
        }
        stage('Quality Gate') {
            steps {
                echo 'Quality Gate Stage'
                quality_gate("${env.SONAR_TOKEN}")
            }
        }
        stage('Image Build') {
            steps {
                dir("${env.TYPE}") {
                    docker_build("${env.DOCKER_USER_NAME}", "${env.REPO_NAME}", "${env.BUILD_ID}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                dir("${env.TYPE}") {
                    docker_push("${env.DOCKER_CRED_ID}", "${env.DOCKER_USER_NAME}/${env.REPO_NAME}", "${env.BUILD_ID}")
                }
            }
        }
    }
    post {
        always {
            cleanWs()
            script {
                sh "echo 'y' | docker system prune -a"
            }
        }
        success{
            build job: 'Upyogi-Frontend-CD', parameters: [
                string(name: 'IMAGE_TAG', value: "${env.BUILD_ID}")
                ]
        }
    }
}
