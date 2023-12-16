pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/vamshikrisha/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '3de51b43-a708-4249-a2a4-2cff0be12686', path: '', url: 'http://172.31.31.101:8080')], contextPath: 'tester', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '3de51b43-a708-4249-a2a4-2cff0be12686', path: '', url: 'http://172.31.19.239:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
