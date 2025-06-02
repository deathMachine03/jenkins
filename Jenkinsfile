pipeline {
    agent { label 'debian' }

    stages {
        stage('Docker version') {
            steps {
                sh "echo $USER"
                sh 'docker version'
            }
        }
        stage('Delete workspace before build starts') {
            steps {
                echo 'Deleting workspace'
                deleteDir()
            }
        }
        stage('Checkout') {
            steps{
                git branch: 'main',
                    url: 'https://github.com/bakavets/docker-lessons.git'        
                }
        }
        stage('Test') {
            steps{
                dir('lesson-1') {
                    sh "ls -la "
                    sh "pwd"
                }
                    sh "ls -la "
                    sh "pwd"
            }
        }
        stage('Build docker image') {
            steps{
                dir('lesson-1') {
                    sh 'docker build -t percyvelle2/jenkins-images:0.6 .'
                }
            }
        }
        stage('Push docker image to DockerHub') {
            steps{
                withDockerRegistry(credentialsId: 'dockerhub-cred-percyvelle2', url: 'https://index.docker.io/v1/') {
                    sh '''
                        docker push percyvelle2/jenkins-images:0.6
                    '''
                }
            }
        }
        stage('Delete docker image locally') {
            steps{
                sh 'docker rmi percyvelle2/jenkins-images:0.4'
            }
        }
    }
}
