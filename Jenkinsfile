pipeline {
    agent any
    tools {
        maven 'MAVEN'
    }
    stages {
        stage('clone') {
            steps {
                git credentialsId: '516bc367-3bd2-481d-80ba-a590a3404bd1', url: 'https://github.com/ArunAkil/python.git'
                echo 'checkout successful';
            }
        }
        stage('compile'){
            steps {
                bat label: '', script: 'mvn compile'
                echo "test successful";
            }
        }
        stage('build') {
            steps {
                bat label: '', script: 'mvn clean'
                bat label: '', script: 'mvn package'
                echo "compile successful";
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
            deploy adapters: [tomcat8(credentialsId: 'd4baff9f-83ff-40ab-a724-16ce0e2c4343', path: '', url: 'http://localhost:8082/')], contextPath: 'python', onFailure: false, war: '**/*.war'
             echo "Deploy successful";
            }
        }
    }
    post {
        always {
            emailext body: 'build successful. view console output ${BUILD_URL}', subject: '${BUILD_JOB} [${BUILD_NUMBER}]', to: 'selvarajselvamani76@gmail.com'
        }
    }
}
