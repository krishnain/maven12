pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                         git 'https://github.com/intelliqittrainings/maven.git' 
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to download the dev code from git repo', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                         sh 'mvn package'    
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'development.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
         stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                         sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.29.204:/var/lib/tomcat9/webapps/testapp.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the QAServer', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                        sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium scripts are failing', cc: '', from: '', replyTo: '', subject: 'Testing  Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
                
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.18.26:/var/lib/tomcat9/webapps/prodapp.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the ProdServers', cc: '', from: '', replyTo: '', subject: 'Delivery  Failed', to: 'delivery.team@gmail.com'
                    }
                }
               
            }
        }
        
        
        
    }
}
