pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Saim0704/Wanderlust-Mega-Project.git'
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
            }
        }
    }
}
