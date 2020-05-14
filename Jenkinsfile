pipeline
{
    agent any
    stages
    {
        stage('Cont Download')
        {
            steps
            {
                git 'https://github.com/shabervali/newmaven.git'
            }
        }
        stage('Cont Build')
        {
            steps
            {
                sh label: '',script: 'mvn package'
            }
        }
        stage('Cont Deploy')
        {
            steps
            {
                sh label: '',script: 'scp /home/ubuntu/.jenkins/workspace/declarativepipeline/webapp/target/webapp.war ubuntu@172.31.14.122:/var/lib/tomcat8/webapps/testenv.war'
            }
        }
        stage('Cont Testing')
        {
            steps
            {
                git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                sh label: '',script: 'java -jar /home/ubuntu/.jenkins/workspace/declarativepipeline/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            sh label: '',script: 'scp /home/ubuntu/.jenkins/workspace/declarativepipeline/webapp/target/webapp.war ubuntu@172.31.8.198:/var/lib/tomcat8/webapps/prodenv.war'
        }
        failure
        {
           mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'jenkins failed', to: 'shabervali006@gmail.com' 
        }
    }
}
