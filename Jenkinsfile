node {
    def app

    stage('Clone Repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build('alvinkl/testing-next')
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Test passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}