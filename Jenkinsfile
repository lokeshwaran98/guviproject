pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy to Dev') {
            when {
                branch 'Dev'
            }
            steps {
                script {
                    sh './Build.sh'
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                        sh 'docker push lokeshwaran98/dev-react-app:latest'
                    }
                }
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                script {
                    sh './Build.sh'
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                        sh 'docker push lokeshwaran98/prod-react-app:latest'
                    }
                }
            }
        }
    }
}
