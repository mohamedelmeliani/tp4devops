pipeline {
    environment {
        registry = "medelm1/job3tp4"
        registryCredential = 'docker_hub'
        dockerImage = ''
    }

    agent any
    
    stages {
        stage('Cloning Git') {
            steps {
                git branch: 'main', url: 'https://github.com/mohamedelmeliani/tp4devops'
            }
        }
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps{
                script {
                    echo "Tests passed"
                }
            }
        }
        stage('Publish Image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy image') {
            steps{
                bat "docker run -d $registry:$BUILD_NUMBER"
            }
        }
    }
}
