node('master') 
{
    stage('ContinuousDownload')
    {
        git 'https://github.com/santoshm-git/maven-1.git'
    }
    stage('ContinuousBuild')
    {
        sh label: '', script: 'mvn package'
    }
    stage('ContinuousDeployment')
    {
        deploy adapters: [tomcat8(credentialsId: '4f4f9772-9e7c-4227-a2a6-04402c640b80', path: '', url: 'http://172.31.18.149:8080')], contextPath: 'test1', war: '**/*.war'
    }
    stage('ContinuousTesting')
    {
       git 'https://github.com/santoshm-git/FunctionalTesting.git' 
       sh label: '', script: 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline/testing.jar'
    }
    stage('ContinuousDelevery')
    {
       deploy adapters: [tomcat8(credentialsId: '4f4f9772-9e7c-4227-a2a6-04402c640b80', path: '', url: 'http://172.31.16.193:8080')], contextPath: 'prod1', war: '**/*.war'
    }
}
