node('Jenkins-Agent') {
    stage('Check Docker') {
        sh 'docker --version'
    }

    stage('Source Code Clone (Git)') {
        checkout scm
    }

    stage('Build-Tag') {
        // Use the docker object only within this stage
        app = docker.build('ameliamae/amalan_car_site')
    }

    stage('Push-To-DockerHub') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            app.push('latest')
        }
    }

    stage('Deploy') {
        sh "docker compose down"
        sh "docker compose up -d"
    }
}
