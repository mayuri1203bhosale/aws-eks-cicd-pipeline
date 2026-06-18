pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "DOCKER_IMAGE = "mayuribhosale/docker-repo-5""
        IMAGE_TAG = "${BUILD_NUMBER}"
        AWS_REGION = "us-east-2"
        CLUSTER_NAME = "cluster1"
        K8S_DIR = "k8s"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/mayuri1203bhosale/aws-eks-cicd-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t $DOCKER_IMAGE:$IMAGE_TAG .
                docker tag $DOCKER_IMAGE:$IMAGE_TAG $DOCKER_IMAGE:latest
                """
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $DOCKER_IMAGE:$IMAGE_TAG
                    docker push $DOCKER_IMAGE:latest
                    """
                }
            }
        }

        stage('Configure AWS & EKS') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-cred'
                ]]) {
                    sh """
                    export AWS_DEFAULT_REGION=$AWS_REGION

                    aws sts get-caller-identity

                    aws eks update-kubeconfig \
                        --region $AWS_REGION \
                        --name $CLUSTER_NAME
                    """
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-cred'
                ]]) {
                    sh """
                    export AWS_DEFAULT_REGION=$AWS_REGION

                    kubectl apply -f /$K8S_DIR/ --validate=false

                    kubectl set image deployment/waso-deployment \
                        waso-container=$DOCKER_IMAGE:$IMAGE_TAG

                    kubectl rollout status deployment/waso-deployment
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Deployment Successful"
        }
        failure {
            echo "Deployment Failed"
        }
    }
}