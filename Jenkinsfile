pipeline {
agent any
environment {
registryCredential = 'dockerhub'
}
stages {
stage('Build') {
steps {
sh 'docker build -t khurram88/frontend-app .'
}
}
stage('Test') {
steps {
sh 'docker container rm node-fe -f || true'
sh 'docker container run -p 8002:8080 --name node-fe -d khurram88/frontend-app'
sh 'sleep 10'   
sh 'curl -I http://localhost:8002'
}
}
stage('Publish') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
sh 'docker push khurram88/frontend-app'
}
}
}
}
}
}
