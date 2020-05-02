node('master') 
{
    stage('Continuous Download') 
    {
    git 'https://github.com/selenium-saikrishna/maven.git'
    }
    stage('Continuous Build') 
    {
    sh label: '', script: 'mvn package'
    }
    stage('Continuous Deployment') 
    {
    sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/Scripted-Pipeline/webapp/target/webapp.war ubuntu@172.31.37.169:/var/lib/tomcat8/webapps/testenv.war'
    }
    stage('Continuous Testing') 
    {
    git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
    sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/Scripted-Pipeline/testing.jar'
    }
    stage('Continuous Delievery') 
    {
    input message: 'Waiting for approval', submitter: 'rahul'
    sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/Scripted-Pipeline/webapp/target/webapp.war ubuntu@172.31.42.216:/var/lib/tomcat8/webapps/prodenv.war'
    }
}
