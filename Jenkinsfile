node('Jenkins-Agent')
{
    def app
    stage('Source Code Clone (Git)'){
        checkout scm
    }

    stage('Build-Tag'){
        app.docker.build('ameliamae/amalan_car_site')
    }

    stage('Push-To-DockerHub'){
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
    }

    stage('Deploy'){
        sh "docker compose down"
        sh "docker compose up -d"
    }
}