pipeline{
    agent any
    environment {
        name = 'dev'
    }
    // parameters{
    //     string(name:'Person',defaultValue:'Dev')
    // }
    stages{
        stage('Test'){
            steps{
                echo 'Testing Code'
                sh 'echo "${name}"'
                // sh 'echo "${Person}"'
            }
        }
        stage('Build'){
            // input{
            //     message "Should we continue?"
            //     ok "Yes we should"
                
            // }
            steps{
                echo 'Building Code'
            }
        }
        stage('Deploy on Test'){
            steps{
                echo 'Deployment on test'
            }
        }
        stage('Deploy on Prod'){
            steps{
                echo 'Deployment on prod'
            }
        }
        stage('Build with JDK 8') {
            tools {
                jdk 'Amazon Corretto' // Name of the JDK as configured in Global Tool Configuration
            }
            steps {
                sh 'java -version'
                // Add build steps here
            }
        }

        stage('Build with JDK 11') {
            tools {
                jdk 'Java 11' // Name of the JDK as configured in Global Tool Configuration
            }
            steps {
                sh 'java -version'
                // Add build steps here
            }
        }
    }
}
