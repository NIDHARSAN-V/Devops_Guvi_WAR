pipeline {
    agent any

    stages {
        stage('Clone Git Repository') {
            steps {
                git 'https://github.com/NIDHARSAN-V/Devops_Guvi_WAR.git'
            }
        }
        
        stage('Build WAR File') {
            steps {
                sh 'mvn clean package'  // Build WAR file using Maven
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t warimage-jenkins .'
                    sh 'docker tag warimage-jenkins nidharsan8008/warimage-jenkins1'
                }
            }
        }
        
        // stage('Run Docker Container') {  // Optional stage to test the container
        //     steps {
        //         script {
        //             sh 'docker run -d -p 8888:8080 --name war-container-jenkins warimage-jenkins'
        //         }
        //     }
        // }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub_token', url: 'https://index.docker.io/v1/') {
                        sh 'docker push nidharsan8008/warimage-jenkins1'
                    }
                }
            }
        }
    }
}
