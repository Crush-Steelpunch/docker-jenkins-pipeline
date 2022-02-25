pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Crush-Steelpunch/todo-app-v4.git']]])
		sh "docker build -t leonrobinson/todapp-pipelinebuild:latest"
		sh "docker tag  leonrobinson/todapp-pipelinebuild:latest    leonrobinson/todapp-pipelinebuild:$BUILD_NUMBER"
            }
        }
        stage('Deploy') {
            steps {
                sh "docker stop todoapppipeline"
                sh "docker rm todoapppipeline"
		sh "docker run -d -p 5001:5000 leonrobinson/todapp-pipelinebuild:latest"
            }
        }
    }
}
