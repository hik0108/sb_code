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
    
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
