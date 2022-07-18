node('nodes')
{
    def mavenhome= tool name:"maven3.8.6"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
    stage('checkout code'){
        git branch: 'development', credentialsId: '7f304c83-947a-4f1a-81c3-a9c27095174c', url: 'https://github.com/kumarnaveentulsai/maven-web-application.git'
    }



    stage('build'){
        sh "${mavenhome}/bin/mvn clean package"
        
    }
    stage('execute sonarqube package'){
         sh "${mavenhome}/bin/mvn clean sonar:sonar"
    }

    stage('upload buildartifact'){
        sh "${mavenhome}/bin/mvn clean deploy"
    }
    stage('tomcat'){
        sshagent(['cc0fb0d2-a3bb-4764-8344-a0bf53d0a4df']) {
        sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.17.68:/opt/apache-tomcat-9.0.64/webapps/"
}
    }
    
    
}
