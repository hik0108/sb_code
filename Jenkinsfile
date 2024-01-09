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
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
