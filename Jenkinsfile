pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/23mh1a0553/stylish.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop my-java-app || true
                docker rm my-java-app || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi tejaswi-maven || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t amazon .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d --name aws -p 8087:8080 amazon'
            }
        }
    }
}
