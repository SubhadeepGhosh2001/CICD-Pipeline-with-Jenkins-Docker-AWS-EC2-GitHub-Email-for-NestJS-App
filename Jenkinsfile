node {

    // ===== Environment variables =====
    env.CONTAINER_NAME = "nestjs-app"
    env.IMAGE_NAME     = "nesths-image"
    env.EMAIL          = "subhadeepghosh1270@gmail.com"
    env.PORT           = "3000"

    stage('Clone Repo') {
        git branch: 'main',
            url: 'https://github.com/SubhadeepGhosh2001/CICD-Pipeline-with-Jenkins-Docker-AWS-EC2-GitHub-Email-for-NestJS-App.git'
    }

    stage('Build Docker Image') {
        sh """
            docker build -t ${env.IMAGE_NAME} .
        """
    }

    stage('Stop & Remove Previous Container') {
        sh """
            docker stop ${env.CONTAINER_NAME} || true
            docker rm ${env.CONTAINER_NAME} || true
        """
    }

    stage('Docker Container Run') {
        sh """
            docker run -d -p ${env.PORT}:${env.PORT} \
            --name ${env.CONTAINER_NAME} \
            ${env.IMAGE_NAME}
        """
    }

    stage('Send Email Notification') {
        emailext(
            subject: "NestJS App Deployed Successfully on EC2!",
            body: "Your NestJS app is Deployed! http://13.232.207.194:${env.PORT}/",
            to: env.EMAIL
        )
    }
}
