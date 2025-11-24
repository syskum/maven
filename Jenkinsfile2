

pipeline
{
    agent any
    stages
    {
        stage('Download')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '8c4a8c6e-136e-430f-b8dd-3365d294c75e', path: '', url: 'http://172.31.31.19:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
         stage('Testing')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '8c4a8c6e-136e-430f-b8dd-3365d294c75e', path: '', url: 'http://172.31.25.180:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
