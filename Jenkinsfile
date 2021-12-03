pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_Loans')
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
        stage('ContinuousBuild_Loans')
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
        
        
        
    }
}
