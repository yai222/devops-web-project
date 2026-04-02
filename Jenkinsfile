pipeline {
    agent any
    
    stages {
        stage('Packaging') {
            steps {
                echo 'Packaging..'
                sh 'mvn clean package'
            }
        }
        stage('Copying war file') {
            steps {
                echo 'Copying war file..'
                sh 'mv target/*.war .'
            }
        }
        stage('cleanup') {
            steps {
                sh 'sudo docker system prune -a --volumes --force --filter "label=devops-web-project-server"'
            }
        }
        stage('build image') {
            steps {
                sh 'sudo docker build -t yai222/devops-web-project:v1 --label devops-web-project-server .'
            }
        }
        stage('run container') {
            steps {
                sh 'sudo docker run -d --name devops-web-project-server --label devops-web-project-server -p 8083:8080 yai222/devops-web-project:v1'
            }
        }
    }
}
