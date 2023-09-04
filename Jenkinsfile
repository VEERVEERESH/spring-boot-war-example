pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("checkout"){
            steps{
                // mvn test
               checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/VEERVEERESH/spring-boot-war-example.git']])
            }
            
        }
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn package"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'f41262ef-ab3a-4ca3-aa20-4f1d80e5261c', path: '', url: 'http://10.0.2.15:8089')], contextPath: '/App', war: '**/*.war'
              
            }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'f41262ef-ab3a-4ca3-aa20-4f1d80e5261c', path: '', url: 'http://10.0.2.15:8089')], contextPath: '/Apps', war: '**/*.war'

            }
        }
    }
}
