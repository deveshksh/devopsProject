pipeline {
    agent any

    environment {
        REGISTRY = 'deveshksh'                          // Docker Hub username
        REGISTRY_CREDENTIALS = 'docker-hub-credentials' // Docker Hub credentials ID in Jenkins
        PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"  // Updated PATH
    }

    stages {
        stage('Test Environment') {
            steps {
                sh 'echo $PATH'
                sh 'which dotnet'
                sh 'dotnet --version'
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/deveshksh/devopsProject.git', branch: 'master', credentialsId: 'github-credentials'
            }
        }

        stage('Build and Test') {
            steps {
                echo "Building and testing the code..."
                sh 'dotnet build store.sln'
                sh 'dotnet test tests/CartMicroservice.UnitTests/CartMicroservice.UnitTests.csproj'
                sh 'dotnet test tests/CatalogMicroservice.UnitTests/CatalogMicroservice.UnitTests.csproj'
                sh 'dotnet test tests/IdentityMicroservice.UnitTests/IdentityMicroservice.UnitTests.csproj'
            }
        }

        stage('Build and Push Docker Images') {
            parallel {
                stage('Catalog Microservice') {
                    steps {
                        script {
                            dockerBuildAndPush('catalog-microservice', 'src/microservices/CatalogMicroservice')
                        }
                    }
                }
                stage('Cart Microservice') {
                    steps {
                        script {
                            dockerBuildAndPush('cart-microservice', 'src/microservices/CartMicroservice')
                        }
                    }
                }
                stage('Identity Microservice') {
                    steps {
                        script {
                            dockerBuildAndPush('identity-microservice', 'src/microservices/IdentityMicroservice')
                        }
                    }
                }
                stage('Frontend Gateway') {
                    steps {
                        script {
                            dockerBuildAndPush('frontend-gateway', 'src/gateways/FrontendGateway')
                        }
                    }
                }
                stage('Backend Gateway') {
                    steps {
                        script {
                            dockerBuildAndPush('backend-gateway', 'src/gateways/BackendGateway')
                        }
                    }
                }
                stage('Frontend') {
                    steps {
                        script {
                            dockerBuildAndPush('frontend-microservice', 'src/uis/Frontend')
                        }
                    }
                }
                stage('Backend') {
                    steps {
                        script {
                            dockerBuildAndPush('backend-microservice', 'src/uis/Backend')
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying microservices..."
                sh '''
                docker-compose down
                docker-compose up -d
                '''
            }
        }
    }
}

def dockerBuildAndPush(serviceName, contextDir) {
    def imageName = "${env.REGISTRY}/${serviceName}:latest"
    withEnv(["IMAGE_NAME=${imageName}", "CONTEXT_DIR=${contextDir}"]) {
        withCredentials([usernamePassword(credentialsId: env.REGISTRY_CREDENTIALS,
                                          usernameVariable: 'DOCKER_USERNAME',
                                          passwordVariable: 'DOCKER_PASSWORD')]) {
            sh '''
            echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
            docker build -t "$IMAGE_NAME" -f "$CONTEXT_DIR/Dockerfile" .
            docker push "$IMAGE_NAME"
            '''
        }
    }
}