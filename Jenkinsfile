@Library('shared') _
pipeline {
    agent any
    environment {
        GIT_REPO_URL = "https://github.com/Saim0704/Wanderlust-Mega-Project.git"
        GIT_BRANCH = "main"
        DOCKER_USER_NAME = "saim0704"
        REPO_NAME = "wanderlust"
        SCANNER_HOME=tool "sonar"
        SONARQUBE_SERVER = "sonar"
        PROJECT_NAME = "Wanderlust-Frontend"
        PROJECT_KEY = "Wanderlust-Frontend"
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
                echo 'Sonar Scanner Stage'
                dir('frontend'){
                    sonar_scanner("${env.SONARQUBE_SERVER}", "${env.PROJECT_NAME}", "${env.PROJECT_KEY}")
                }
            }
        }
        stage('Quality Gate') {
            steps {
                echo 'Quality Gate Stage'
            }
        }
        stage('Image Build') {
            steps {
                dir('frontend') {
                    docker_build("${env.DOCKER_USER_NAME}", "${env.REPO_NAME}", "${env.BUILD_ID}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                dir('frontend') {
                    docker_push("${env.CREDENTIALS_ID}", "${env.DOCKER_USER_NAME}/${env.REPO_NAME}", "${env.BUILD_ID}")
                }
            }
        }
    }
}
