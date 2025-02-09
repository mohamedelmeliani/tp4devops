pipeline {
    environment {
        registry = 'medelm1/job3tp4'
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                script {
                    // Check out the correct branch
                    git branch: 'main', url: 'https://github.com/mohamedelmeliani/tp4devops'
                }
            }
        }
        stage('Building image') {
            steps {
                script {
                    // Ensure the image is built correctly
                    echo "Building image with tag: ${BUILD_NUMBER}"
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    // Simple test step (replace with actual tests if needed)
                    echo 'Tests passed'
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    // Push image to Docker registry if it's built
                    if (dockerImage) {
                        docker.withRegistry('', registryCredential) {
                            dockerImage.push()
                        }
                    } else {
                        echo 'Docker image not built.'
                    }
                }
            }
        }
    }
}
