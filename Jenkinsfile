pipeline {
    agent any

    stages {
        stage('Cloning Git Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/luisrigo2005/jk-public-gh.git'
            }
        }
        
        stage('Buildin Image') {
            steps {
                sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }
        
        stage('Deploying Application') {
            steps {
                sh '''
                docker stop webapp_ctr || true
                docker rm webapp_ctr || true
                docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
            '''
            }
        }
    }
}
