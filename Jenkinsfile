@Library('sharedLibJenkins') _

pipeline {
    agent any
    
    environment {
        GITHUB_REPO = 'https://github.com/Abdullah-0-3/chattingo'
        BRANCH = 'dev'
        DOCKER_FRONTEND_IMAGE = 'muhammadabdullahabrar/chattingo-frontend'
        DOCKER_BACKEND_IMAGE = 'muhammadabdullahabrar/chattingo-backend'
        DOCKERHUB_CREDENTIALS = 'dockerhub-credentials'
    }
    
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        
        stage('Pull GitHub Repo') {
            steps {
                git branch: "${BRANCH}", url: "${GITHUB_REPO}"
            }
        }
        
        stage('Get Build Number') {
            steps {
                script {
                    env.DOCKER_TAG = "${BUILD_NUMBER}"
                    echo "Build Number: ${env.DOCKER_TAG}"
                }
            }
        }
        
        stage("Docker Images") {
            parallel {
                stage ("Building Frontend Docker Image") {
                    steps {
                        dir("./frontend") {
                            dockerBuild(
                                imageName: env.DOCKER_FRONTEND_IMAGE,
                                imageTag: env.DOCKER_TAG,
                                dockerfile: "Dockerfile",
                                context: "."
                            )
                        }
                    }
                }
                stage ("Building Backend Docker Image") {
                    steps {
                        dir("./backend") {
                            dockerBuild(
                                imageName: env.DOCKER_BACKEND_IMAGE,
                                imageTag: env.DOCKER_TAG,
                                dockerfile: "Dockerfile",
                                context: "."
                            )
                        }
                    }
                }
            }
        }
        
        stage("Push Docker Images") {
            parallel {
                stage ("Pushing Frontend Docker Image") {
                    steps {
                        dir("./frontend") {
                            dockerPush(
                                imageName: env.DOCKER_FRONTEND_IMAGE,
                                imageTag: env.DOCKER_TAG,
                                credentials: env.DOCKERHUB_CREDENTIALS
                            )
                        }
                    }
                }
                stage ("Pushing Backend Docker Image") {
                    steps {
                        dir("./backend") {
                            dockerPush(
                                imageName: env.DOCKER_BACKEND_IMAGE,
                                imageTag: env.DOCKER_TAG,
                                credentials: env.DOCKERHUB_CREDENTIALS
                            )
                        }
                    }
                }
            }
        }
    }
}