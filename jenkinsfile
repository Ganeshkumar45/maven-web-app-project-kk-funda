pipeline {
    
    agent any
    
    tools
    {
        maven "maven"
    }
    
    stages {
        
        
        stage ('checkout stage') {
            
            steps 
            {
                git branch: 'DEV', credentialsId: '7788625b-3237-4c9c-85db-c7a209ec1085', url: 'https://github.com/venkatravuru/maven-web-app-project-kk-funda.git'
            }
        }
        stage ('maven compile') {
            
         steps 
         {
             sh 'mvn clean compile'
         }
       }
       stage ('maven build') {
           steps 
           {
               sh 'mvn clean package'
           }
       }
       stage ('Code Analysis') {
           steps 
           {
               sh 'mvn clean sonar:sonar'
           }
       }
       stage ('Deploy to Nexus') {
           steps
           {
               sh 'mvn clean deploy'
           }
       }
       stage ('deploy app') {
           steps
           {
        sh """
            curl -u admin:venkat123\
            --upload-file /var/lib/jenkins/workspace/multibranch_pipeline/target/maven-web-application.war \
            "http://http://18.61.33.87:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
           }
       }
    }
}
