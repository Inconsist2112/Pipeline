pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
               // slackSend channel: 'youtubejenkins', message: 'Job Started'
                
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn install"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                //deploy adapters: [tomcat9(credentialsId: 'TomcatTestEnv', path: '', url: 'http://3.6.93.25:8080')], contextPath: '/app', war: '**/*.war'
            deploy adapters: [tomcat9(credentialsId: 'tomcat2', path: '', url: 'http://13.233.179.204:8080')], contextPath: '/app', war: '**/*.war'
                
deploy adapters: [tomcat9(credentialsId: 'tomcat2', path: '', url: 'http://65.2.4.99:8080')], contextPath: '/app', war: '**/*.war'
            }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container -> plugin
            // deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://52.66.208.45:8080')], contextPath: '/app', war: '**/*.war'
                deploy adapters: [tomcat9(credentialsId: 'tomcatProd', path: '', url: 'http://52.66.208.45:8080')], contextPath: '/app', war: '**/*.war'
                echo "DEPLOY ON PROD"
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
           //  slackSend channel: 'youtubejenkins', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
          //   slackSend channel: 'youtubejenkins', message: 'Job Failed'
        }
    }
}
