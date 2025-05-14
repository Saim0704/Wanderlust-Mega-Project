@Library('shared') _
pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                script{
                    git_checkout("https://github.com/Saim0704/Wanderlust-Mega-Project.git", "main")
                }
            }
        }
        stage('Sonar Scanner') {
            steps {
                echo 'Sonar Scanner Stage'
            }
        }
        stage('Quality Gate') {
            steps {
                echo 'Quality Gate Stage'
            }
        }
        stage('Image Build') {
            steps {
                echo 'Build Stage'
                docker_build("saim0704", "wanderlust", "${env.BUILD_ID}")
            }
        }
    }
}
