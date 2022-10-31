pipeline {
    agent any
    tools {
        maven 'MAVEN'
        jdk ''
    }
    stages {
        stage('clone') {
            steps {
                git credentialsId: 'Santhosh-Nagarajan/******(git credential)', url: 'https://github.com/Santhosh-Nagarajan/demo-jar.git'
                echo 'checkout successful';
            }
        }
        stage('compile'){
            steps {
                bat label: '', script: 'mvn compile'
                echo "test successfully";
            }
        }
        stage('build') {
            steps {
                bat label: '', script: 'mvn clean'
                bat label: '', script: 'mvn package'
                echo "compile successfully";
            }
        }
        stage('test'){
            steps {
               bat label: '', script: 'mvn test'
               echo "test successful";
            }
        }
        stage ('Deploy') {
            steps{
            deploy adapters: [tomcat10(path: '', url: 'http://localhost:8090/')], contextPath: 'pythonfile', onFailure: false, jar: '**/*.jar'
             echo "Deploy successfully";
            }
        }
    }
   
}
