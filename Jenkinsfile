pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '42341f92-daf0-494d-b2e8-379bbdb2a05f', path: '', url: 'http://172.31.15.40:8080')], contextPath: 'test1', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '42341f92-daf0-494d-b2e8-379bbdb2a05f', path: '', url: 'http://172.31.14.104:8080')], contextPath: 'prod11', war: '**/*.war'
            }
        }
    }
}
