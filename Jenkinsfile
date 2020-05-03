pipeline
{
    agent any
    stages
    {
        stage('ContiniousDownload')
        {
            steps
            {
                git 'https://github.com/awsrahulgupta/scriptedpipeline.git'
            }
        }
        stage('ContiniousBuild')
        {
            steps
            {
                sh label: '', script: 'mvn package'
            }
        }
        stage('ContiniousDeployment')
        {
            steps
            {
               sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/Scripted-Pipeline/webapp/target/webapp.war ubuntu@172.31.37.169:/var/lib/tomcat8/webapps/testenv.war'
            }
        }
        stage('ContiniousTesting')
        {
            steps
            {
                git 'https://github.com/awsrahulgupta/functionaltesting.git'
    sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/Scripted-Pipeline/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/Scripted-Pipeline/webapp/target/webapp.war ubuntu@172.31.42.216:/var/lib/tomcat8/webapps/prodenv.war'
        }
        failure
        {
            mail bcc: '', body: 'Jenkins Failed at X stage, please take necessary action.', cc: '', from: '', replyTo: '', subject: 'Jenkins Failed', to: 'awsrahulgupta@gmail.com'
        }
    }
}
