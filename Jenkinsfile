node {
    
    stage('SCM Check out'){
        git 'https://github.com/mudesouky/flask-hello-world'
    }
    stage('Docker Build'){
        sh 'docker build -t desouky/flaskapp .'
    }
    stage('Docker Push'){
        withCredentials([string(credentialsId: 'DockerHubPassword', variable: 'DockerHubPW')]) {
            sh "docker login -u desouky -p ${DockerHubPW}"
        }
        sh 'docker push desouky/flaskapp'
    }
    stage('Deploy Stack'){
        sh 'docker stack deploy -c docker-compose.yml cognitev'
    }
    stage('Clean Up'){
        sh 'docker system prune -f'
    }
    
}
