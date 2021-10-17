node{
    
    def mavenHome = tool name: "maven3.8.2"
    stage('checkoutcode'){
        git branch: 'development', credentialsId: '0a1de688-ca95-492e-8b4f-fc181c28a4a1', url: 'https://github.com/radha-devops/maven-web-application.git'
    }
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSonarQubeReport'){
        sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    stage('UploadArtifactIntoNexuxRepo'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('DeploytheAppIntoTomcat'){
        sshagent(['e0068cdd-4ecf-4fe3-97c9-b802a29c1eef']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-appliocation.war ec2-user@13.233.207.116:/opt/apache-tomcat-9.0.53/webapps"
    }
    }
    stage('SendEmailNotification'){
        mail bcc: 'radha.deoghare724@gmail.com', body: '''Build Over regards. RD''', cc: 'radha.deoghare724@gmail.com', from: '', replyTo: '', subject: 'Build Over!', to: 'radha.deoghare724@gmail.com'
    }
}
