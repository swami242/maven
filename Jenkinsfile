pipeline
{    
    agent any
    stages
    {
        stage('contdownload')
        {
            steps 
            {  
               git https://github.com/swami242/maven.git
            } 
        }    
        stage('contBuild')
        {
            steps 
            {  
               sh 'mvn package'
            }
        }
        stage('contDeployment')
        {
            steps 
            {  
               deploy adapters: [tomcat9(credentialsId: '31fbcc73-4dce-45a2-85f2-3e3195c8a229', path: '', url: 'http://172.31.24.199:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('contTesting')
        {
            steps 
            {  
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline2/testing.jar'
               
            }
        }
        stage('contDelivery')
        {
            steps
            {
               input message: 'Need aproval from DM!', submitter: 'prasad'
               deploy adapters: [tomcat9(credentialsId: '31fbcc73-4dce-45a2-85f2-3e3195c8a229', path: '', url: 'http://172.31.30.171:8080')], contextPath: 'prodapp', war: '**/*.war'   
            }
        
         }
    }
}
