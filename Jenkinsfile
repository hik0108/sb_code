pipeline {
    agent any
    
    tools {
        maven 'my_maven'
    }
    environment {
        GITNAME = 'hik0108'
        GITEMAIL = 'dlsrud0723@naver.com'
        GITWEBADD = 'https://github.com/hik0108/sb_code.git'
        GITSSHADD = 'git@github.com:hik0108/sb_code.git'
        GITCREDENTIAL = 'git_cre'
        
        DOCKERHUB = 'hinkyung/spring'
        DOCKERCREDENTIAL = 'docker_cre'
    }
    stages {
        stage('checkout Github') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [],
                userRemoteConfigs: [[credentialsId: GITCREDENTIAL, url: GITWEBADD]]])
            }
            
        post {
        
            failure {
                echo 'Repository clone failure'
            }
            success {
                echo 'Repository clone success'
            }
        }
    }

        
        stage('code build') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('image build') {
            steps {
                sh "docker build -t ${DOCKERHUB}:${currentBuild.number} ."
                sh "docker build -t  ${DOCKERHUB}:latest ."
                // currentBuild.number : 젠킨스 build number
            }
        }
        stage('image push') {
            steps {
                sh "docker  push ${DOCKERHUB}:${currentBuild.number}"
                sh "docker  push ${DOCKERHUB}:latest"
                // currentBuild.number : 젠킨스 build number
            }
            
            post {
                failure {
                    echo 'docker image push failure'
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                }
                
                success{
                    echo 'docker image push success'
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                }
            }
        }
        
    }
}
