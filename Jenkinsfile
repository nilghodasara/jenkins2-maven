pipeline {
    agent any
    tools {
        maven 'maven3.9'
        jdk 'java17'
    }
    stages {
        stage('git-dow-code') {
            steps {
                echo "downloding code from git"
                git branch: 'main', url: 'https://github.com/nilghodasara/jenkins2-maven.git'
            }
        }
        stage('build') {
            steps {
                echo "hello"
                sh 'mvn clean package'
            }
        }
        stage('test-case') {
            steps {
                echo "nil"
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
            }
        }
        stage('archive') {
            steps {
                echo 'hello'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Deploy') {
            steps {
                echo 'hello'
                deploy adapters: [tomcat9(credentialsId: 'tomcatnamecred', path: '', url: 'http://34.125.3.230:8090/')], contextPath: null, war: '**/*.war'
            }
        }
        stage('post-build-action') {
            steps {
                echo 'hello'
                build wait: false, job: 'deploy-to-dev-pipeline'
            }
        }
    }
}
