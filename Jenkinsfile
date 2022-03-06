pipeline
{
    agent any
    stages
    {
        stage('continuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                         git 'https://github.com/krishnain/maven.git' 
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins failed to download from remote github', cc: '', from: '', replyTo: '', subject: 'Download failed ', to: 'gitadmin@gmail.com'
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
                        http://50.17.28.74:8080/job/DeclarativePipeline/pipeline-syntax/#:~:text=mail%20bcc%3A%20%27%27%2C%20body%3A%20%27maven%20unable%20to%20read%20and%20convert%20code%20into%20artifact%27%2C%20cc%3A%20%27%27%2C%20from%3A%20%27%27%2C%20replyTo%3A%20%27%27%2C%20subject%3A%20%27Build%20failed%20%27%2C%20to%3A%20%27devad%40gmail.com%27
                        exit(2)
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
                       deploy adapters: [tomcat9(credentialsId: '50b92e83-9ad4-4da2-8873-e76971b1f6b3', path: '', url: 'http://54.82.29.70:8080')], contextPath: 'Testapp', war: '**/*.war'  
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins unable to deploy to tomcats server ', cc: '', from: '', replyTo: '', subject: 'deployment Failed ', to: 'midteam@gmail.com'
                        exit(3)
                    }
                }
               
            }
        }
        stage('ContinousTesting')
        {
            steps
            {
                script 
                {
                    try
                    {
                               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar' 
                    }
                    catch(Exception e4)
                    {
                 mail bcc: '', body: 'selenium scripts are failing ', cc: '', from: '', replyTo: '', subject: 'Testing Failed ', to: 'test.team@gmail.com'
                        exit(4)
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
                        deploy adapters: [tomcat9(credentialsId: '50b92e83-9ad4-4da2-8873-e76971b1f6b3', path: '', url: 'http://172.31.18.225:8080')], contextPath: 'Testapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins unable to deploy into tomcat on prodserver ', cc: '', from: '', replyTo: '', subject: 'Testing Failed ', to: 'delivery.team@gmail.com'
                    }
                }
                
            }
        }
    }
}
