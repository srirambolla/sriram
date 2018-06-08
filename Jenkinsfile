pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                withMaven(maven : 'M3'){
                sh 'mvn clean compile'
                }
            }
        }
        stage('Test') { 
            steps {
               withMaven(maven : 'M3'){
                sh 'mvn test'
                } 
            }
        }
        stage('Deploy') { 
            steps {
                withMaven(maven : 'M3'){
                sh 'mvn deploy'
                }
                
            }
        }
    }
}
