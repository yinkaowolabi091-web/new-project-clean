pipeline {
    agent any

   environment {
    FRONTEND_IMAGE= "mern-frontend:jenkins"
    BACKEND_IMAGE= "mern-backend:jenkins"
    PORT="5000"
    MONGO_URI="mongodb://mongo:27017/taskdb"
    }
    stages{
        stage('Checkout Code'){
            steps{
                git url: 'https://github.com/yinkaowolabi091-web/new-project-clean.git', branch: 'main'
            }
        }
        stage('Prepare .env'){
            steps{
                sh '''
                   mkdir -p server
                   cat > server/ .env <<EOF
PORT=${PORT}
MONGO_URI=${MONGO_URI}
EOF
                '''
            }
        }
        stage('Build docker images'){
            steps{
                sh'''
                echo 'Building docker image...'
                docker build -t $BACKEND_IMAGE ./server

                echo 'Building frontend image...'
                docker build -t $FRONTEND_IMAGE ./client --build-arg VITE_API_URL=http://localhost:$5000/api
                '''
            }
        }
        stage('rUN WITH DOCKER COMPOSE'){
            steps{
                sh'''
                echo 'Starting services with Docker Compose...'
                docker-compose up -d

                echo "showing running containers..."
                docker ps
                '''
            }
        }
    }
}
